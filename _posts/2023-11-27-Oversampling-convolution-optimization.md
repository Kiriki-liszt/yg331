---
title:   "Oversampling 이야기 - convolution optimization"
excerpt: "플러그인 오버샘플링 이야기"
date:  2023-11-27 00:12:00 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## convolution optimization  

Oversampling에 사용하는 FIR 필터는 홀수 개의 대칭 tap을 가진다.  
따라서, convolution을 할 때 coef*(buff+buff)의 형태로 계산한다면 곱연산의 수를 절반 가량 줄일 수 있다.  

또한 SIMD 최적화를 통해 두 개의 double 연산을 동시에 할 수 있다. 이는 SSE2 기반이므로 현재 음악 작업에 사용되는 거의 모든 컴퓨터에서 작동할 것이다.  
메모리의 align이 되어 있어야 하므로 구조체 버퍼 등의 생성 시 alignas(16) 등으로 정렬해준다.  
이 기법을 fir 필터의 대칭성 최적화와 같이 사용하기 위해서는 input이 buffer에 들어갈 때 정렬이 깨지지 않도록 주의를 기울여야 한다.  

``` c++
// 4 in 1 out
void GUI_Processor::Fir_x4_dn(Vst::Sample64* in, Vst::Sample64* out, int32 channel)
{
  // SSE + Symmetry
  double inter_41[2];
  int half_tap = 96; // dnTap_42 / 2;
  // 102 = half_tap +1(addr0) + 1(addr101) + 4(4x1 dnsample)

  size_t _100_192 = sizeof(double) * 93;
  memmove(dnSample_42[channel].buff + 100 + 1 + 1 + 4, dnSample_42[channel].buff + 100 + 1 + 1, _100_192);

  size_t _96_99 = sizeof(double) * 4; // dest: (101:na) added
  memmove(dnSample_42[channel].buff + 96 + 1 + 1 + 4, dnSample_42[channel].buff + 96 + 1, _96_99);

  size_t _0_95 = sizeof(double) * 96;
  memmove(dnSample_42[channel].buff + 1 + 4, dnSample_42[channel].buff + 1, _0_95);

  dnSample_42[channel].buff[4] = in[0]; // buff[3]
  dnSample_42[channel].buff[3] = in[1];
  dnSample_42[channel].buff[2] = in[2];
  dnSample_42[channel].buff[1] = in[3];

  __m128d _acc_out_a = _mm_setzero_pd();
  for (int i = 0; i < half_tap; i += 2) {
    __m128d coef_a = _mm_load_pd(&dnSample_42[channel].coef[i]);
    __m128d buff_a = _mm_load_pd(&dnSample_42[channel].buff[i + 4]);
    __m128d buff_b = _mm_loadr_pd(&dnSample_42[channel].buff[dnTap_42 + 4 - 1 - i]);
    //__m128d buff_b = _mm_set_pd(dnSample_42[channel].buff[dnTap_42 + 4 - 1 - i ], dnSample_42[channel].buff[dnTap_42 + 4 - 1 - i+1]);
    buff_a = _mm_add_pd(buff_a, buff_b);
    __m128d _mul_a = _mm_mul_pd(coef_a, buff_a);
    _acc_out_a = _mm_add_pd(_acc_out_a, _mul_a);
  }
  _mm_store_pd(inter_41, _acc_out_a);
  *out = inter_41[0] + inter_41[1] + dnSample_42[channel].coef[half_tap] * dnSample_42[channel].buff[half_tap + 4];
  return; 
}

```
