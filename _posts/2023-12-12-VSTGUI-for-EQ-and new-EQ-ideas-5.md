---
title:   "VSTGUI와 EQ curve, 그리고 새로운 EQ - 5"
excerpt: "플러그인 이야기"
date:  2023-12-12 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## N-th order pass filters  

12dB/oct보다 더 높은 차수의 필터가 필요할 때, 여러 6dB/oct와 12dB/oct 필터들을 조합하여 얻을 수 있다.  
일반적으로 EQ에 사용하는 n-th order는 Butterworth를 따른다.  
<https://en.wikipedia.org/wiki/Butterworth_filter>  

이때, 필터의 응답은 cascade하여 구하고, Magnitude 응답은 곱하여 구한다.  

## Oversampling and Low-end Phase  

이상적인 Highpass의 응답은 다음과 같다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_ideal_freq_1.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_ideal_phase_1.png){: .align-center}  

하지만, 오버샘플링을 하는 경우 Stopband의 ripple이 남기 때문에 Phase 응답이 꼬이게 된다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_phase_2.png){: .align-center}  

그렇다고 Highpass만 Oversampling을 하지 않는다면 Curve가 변형되고 target frequency가 변할 위험이 있다.  

결국 Fir window를 바꾸거나, att. level, transition band width를 바꿔가며 적절한 세팅을 찾으면 된다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_result.png){: .align-center}  

Kaiser-Bessel window의 경우, 255 tap, 1/4 band, -219.99dB의 세팅에서 -200dB의 감쇠를 보인다.  

albrecht-7 term, 255 tap, 1/4 band의 세팅에서 -208dB의 감쇠를 얻을 수 있지만, Fold-back이 일어나는 지점에서 완벽한 직선의 형태로 crossover가 일어나지 않아 사용하지 않았다.  
이는 나중에 sidechain이나 pararell mix용으로 사용하면 좋을 것 같다.  

## Oversampling and Stop-band noise  

오버샘플링에 사용하는 FIR 필터들은 stopband att. level이 존재하여 Non-harmonic noise가 된다.  
그래서 일반적인 상황에서는 잘 들리지 않지만, 극단적인 Highpass시 낮은 주파수 영역에 나타난다.  

즉, 이를 염두에 두지 않는다면 Highpass시 맨 아래에 slope가 유지되지 않고 shelving EQ가 되어버린다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_ideal_vs_noise.png){: .align-center}  

FabFilter Pro-Q 3의 경우 Natural phase mode에서 비교적 높은 tap 수를 통해 -200dB 이하로 낮추었다.  
이를 harmonic inspect탭에서 관찰하면 -300dB 이하까지 낮춘 것을 확인할 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_Pro-Q3.png){: .align-center}  

Ozone 10 EQ의 경우, -150dB 정도의 noise floor를 가지고 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_Ozone.png){: .align-center}  

Crave EQ의 경우, -180dB 정도의 noise floor를 가지고 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_crave_analog.png){: .align-center}  

DMG Audio의 경우, Fir tap 수에 따라 noise floor가 낮아지는 것을 비교하여 볼 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_DMG_fir_1.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_DMG_fir_2.png){: .align-center}  

## Conclusion  

상기한 Kaiser-Bessel 세팅을 적용하고, Highpass 주파수를 제한한다면 다음과 같이 상한값에서도 Slope를 유지함을 볼 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_result_freq.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-12/Highpass_result_phase.png){: .align-center}  

Phase 응답이 이상해 보이지만, Overshoot 때문에 조금 넘어간 것이지 결국 3 Pi radian으로 수렴한다.  
