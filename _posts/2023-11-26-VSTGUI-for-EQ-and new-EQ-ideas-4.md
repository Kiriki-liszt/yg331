---
title:   "VSTGUI와 EQ curve, 그리고 새로운 EQ - 4"
excerpt: "플러그인 이야기"
date:  2023-11-26 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## Filters - Andy Simper's SVF  

사용한 필터는 Andy의 SVF로 "Simultaneous solving of all outputs of Linear SVF using trapezoidal integration in state space form", "Linear Trapezoidal State Variable Filter SVF in state increment form: state += val" 두 레포트에 기반하였다.  
이것이 기존의 "Solving the continuous SVF equations using trapezoidal integration and equivalent currents"과 다른 점은 캐퍼시터의 state를 갱신할 때 완전히 새로 계산하지 않고, 기존의 값에 더하는 식(state += val)으로 갱신하는 것이다.  
그는 이러한 방식의 이점을  
> "Putting it in the form of a state increment keeps the all coefficients near zero at low frequencies,
which is feels intuitively right to me since you just increment a bit of signal onto your existing state to
do your integration."  
> "state의 갱신을 increment 방식으로 함으로서 낮음 음역대의 필터 계수를 0에 가깝게 유지할 수 있고, 캐퍼시터의 적분을 수행할 때 기존의 state에 신호를 조금 축적해나가는 방식이 자연스럽기 때문이다."  

이라고 설명했다.  

그가 제안한 SVF 필터는 2-pole 2-zero 방식으로 12dB/Oct 커브를 가진다.  
나는 여기에 SVF 6dB filter를 새롭게 추가하여 더 완만한 커브를 쉽게 얻을 수 있는 편의성과 더했다.  

## calc of coefs  

```c++
void makeSVF()
{
  A = pow(10.0, dB / 40.0);
  w = Hz * M_PI / Fs;
  g = tan(w);
  k = 1 / Q;
  s = sqrt(2) / log2(Q + 1);

  double kdA = k / A;
  double kmA = k * A;
  double smA = s * A;
  double gdA = g / sqrt(A);
  double gmA = g * sqrt(A);
  double AmA = A * A;

  switch (type)
  {
  case kLP:    m0 = 0;   m1 = 0;   m2 = 1;   break;
  case kHP:    m0 = 1;   m1 = 0;   m2 = 0;   break;
  case kBP:    m0 = 0;   m1 = 1;   m2 = 0;   break;
  case kNotch: m0 = 1;   m1 = 0;   m2 = 1;   break;
  case kBell:  g = g;   k = kdA; m0 = 1;   m1 = kmA; m2 = 1;   break;
  case kLS:    g = gdA; k = s;   m0 = 1;   m1 = smA; m2 = AmA; break;
  case kHS:    g = gmA; k = s;   m0 = AmA; m1 = smA; m2 = 1;   break;
  default: break;
  }

  if (_6dB) {
    if (type == kLS) { g = tan(w) / A; m0 = 1;   m1 = 0; m2 = AmA; }
    if (type == kHS) { g = tan(w) * A; m0 = AmA; m1 = 0; m2 = 0;   }
    k = 1 - g;
  }

  gt0 = 1 / (1 + g * (g + k));
  gk0 = (g + k) * gt0;
  gt1 = g * gt0;
  gk1 = g * gk0;
  gt2 = g * gt1;
  return;
};
```

이 부분은 주어진 paper를 잘 읽으면 쉽게 구현 가능하다.  

하나 참고할 점은 shelf의 Q = slope 변환이다.  
나는 parameter를 bell을 기준으로 잡았기 때문에 그 범위가 0.5에서 24까지 넓게 변한다.  
이 Q를 그대로 shelf에 넣으면 실용적으로 사용하기 어렵다. 이 표기법을 따르면 sweet spot은 4를 넘어가지 않기 때문이다.  
따라서 Q = 1 => slope = sqrt(2)를 기준으로 1/log2(Q+1)를 취해 적절히 변환하였다.  

다른 하나는 상기한 6dB/oct 필터의 state space form 설계이다.  
gt0 = 1 / (1 + g)가 되도록 k를 고정하고, shelf는 HP + LP*A*A, LP + HP*A*A로 구하였다.  

## compute SVF  

```c++
Steinberg::Vst::Sample64 computeSVF
(Steinberg::Vst::Sample64 input)
{
  if (_6dB) {
    v1 = input;
    v2 = gt1 * input + gt0 * ic1eq;
    v0 = gt0 * input - gt0 * ic2eq;

    ic1eq += 2.0 * g * (input - v2);
    ic2eq += 2.0 * g * v0;

    return m0 * v0 + m1 * v1 + m2 * v2;
  }
    
  t0 = input - ic2eq; 
  v0 = gt0 * t0 - gk0 * ic1eq;
  t1 = gt1 * t0 - gk1 * ic1eq;
  t2 = gt2 * t0 + gt1 * ic1eq;
  v1 = t1 + ic1eq;
  v2 = t2 + ic2eq;
  ic1eq += 2.0 * t1; 
  ic2eq += 2.0 * t2;

  return m0 * v0 + m1 * v1 + m2 * v2;
};
```

이 부분 또한 주어진 paper들을 잘 읽어보면 나온다.  
겁 먹지 말자.  

6dB/oct 필터는 "Direct Numerical Integration of a One Pole Linear Low Pass Filter"에 나온 예제를 가지고 HP를 설계한 뒤,  

> iceq = v - iceq  

형태를 잘 치환하여

> iceq += 2 g v  

형태로 변환할 수 있다.  

## Transfer function of SVF Filters, state increment form  

``` c++
double mag_response(double freq) {
  if (!In) return 1.0;

  double ONE_OVER_SAMPLE_RATE = 1.0 / Fs;

  // exp(complex(0.0, -2.0 * pi) * frequency / sampleRate)
  double _zr = ( 0.0       ) * freq * ONE_OVER_SAMPLE_RATE;
  double _zi = (-2.0 * M_PI) * freq * ONE_OVER_SAMPLE_RATE;

  // z = zr + zi;
  double zr = exp(_zr) * cos(_zi);
  double zi = exp(_zr) * sin(_zi);

  double nr = 0, ni = 0;
  double dr = 0, di = 0;

  if (_6dB != 0) {
    // Numerator complex
    nr = zr * (-m0 + m1 * (g - 1) + m2 * g) + (m0 + m1 * (g + 1) + m2 * g);
    ni = zi * (-m0 + m1 * (g - 1) + m2 * g);

    // Denominator complex
    dr = zr * (g - 1) + (g + 1);
    di = zi * (g - 1);
  }
  else {
    // z * z
    double zsq_r = zr * zr - zi * zi;
    double zsq_i = zi * zr + zr * zi;
  
    double gsq = g * g;

    // Numerator complex
    double c_nzsq = (m0      + m1 *  g + m2 *       gsq);
    double c_nz   = (m0 * -2           + m2 * 2.0 * gsq);
    double c_n    = (m0      + m1 * -g + m2 *       gsq);
    nr = zsq_r * c_nzsq + zr * c_nz + c_n;
    ni = zsq_i * c_nzsq + zi * c_nz;

    // Denominator complex
    double c_dzsq = ( 1 + k *  g +       gsq);
    double c_dz   = (-2          + 2.0 * gsq);
    double c_d    = ( 1 + k * -g +       gsq);
    dr = zsq_r * c_dzsq + zr * c_dz + c_d;
    di = zsq_i * c_dzsq + zi * c_dz;
  }


  // Numerator / Denominator
  double norm = dr * dr + di * di;
  double ddr = (nr * dr + ni * di) / norm;
  double ddi = (ni * dr - nr * di) / norm;

  return sqrt(ddr * ddr + ddi * ddi);
}
```

이는 SVF의 최종 출력인 out = m0*v0 + m1*v1 + m2*v2를 입력 input으로 나누어 준 전달함수이다.  
이때, iceq 항에 z^-1 이 붙으므로 iceq를 v와 input으로 나타낸 후 z = re(z) + im(z)의 형태로 치환하여 풀어내면 특정 주파수에 대한 전달함수가 만들어지고, 이 출력을 CView의 y에 적절히 넣으면 된다.  
