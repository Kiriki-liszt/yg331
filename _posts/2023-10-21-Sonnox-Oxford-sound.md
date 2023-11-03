---
title:   "Sonnox Oxford - harmonics"
excerpt: "플러그인  분석"
date:  2023-11-03 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 시작하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/intro.png){: .align-center}  

Sonnox Oxford 플러그인들은 20년이 넘도록 많은 프로들이 사용하였고, 검증되었다.  
그 중 가장 유명한 Inflator의 배음 생성 특징을 Dynamics, Limiter의 warmth, enhence와 비교해보았다.  

## Oxford Inflator  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/Sonnox_Inf_UI.png){: .align-center}  

비교적 간단한 waveshaper로 odd harmonic을 추가한다.  
0dB 초과시 파형이 접히는 wavefolding 특징 또한 있다.  
더 자세한 설명은 이전 포스트에 있다.  
<https://kiriki-liszt.github.io/yg331/vst/saturation/sonnox-inflator-copy/>  

## Oxford Dynamics - warmth  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/Sonnox_Dyn_UI.png){: .align-center}  

다이나믹스를 정리하는 플러그인이지만, 맨 끝단에 warmth 섹션이 있어 하모닉스를 추가할 수 있는 곳이 있다.  
이 부분만 작동시켜보면 +6dB 안에서 Inflator의 curve-50 세팅과 동일하게 동작한다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/PD_Dyn_Inf_norm_wave.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/PD_Dyn_Inf_norm_time.png){: .align-center}  

+6dB를 벗어나면 Inflator는 Hard Clipping되지만 Dynamics는 원 신호를 그대로 가져온다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/PD_Dyn_Inf_full_wave.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/PD_Dyn_Inf_full_time.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/PD_Inf_full_time.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Dyn-Inf/PD_Dyn_full_time.png){: .align-center}  

## Oxford Limiter - enhence  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/Sonnox_Lim_UI.png){: .align-center}  

하지만 Limiter의 enhence 섹션은 Inflator와 완전히 다르다.  
피크 방지나 청감 음압 상승은 동일하지만, static한 Inflator와 달리 스테레오 채널 간 간섭과 시간-종속적인 부분도 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lin_Inf_norm_wave.png){: .align-center}  

보다시피 enhence는 극적인 sample-waveshaping이 보이지 않는다.  
하지만 큰 입력이 감소된 출력으로 이어지는 특징은 look-ahead 컴프레서와 비슷하다.  
실제로도 이 플러그인은 3ms 정도의 레이턴시를 가지고 있어 Aliasing이 제어되고 있다. 이는 TDR, Waves R-comp/R-vox 등에서도 보이는 특징이다.  

아래의 Hammerstein 분석에서 두 번째 사진인 Limiter의 Harmonics들이 제어되어 저음에는 나타나지만 고음으로 갈 수록 줄어드는 것을 알 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Inf_ham.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_ham.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_Inf_ham.png){: .align-center}  

이어서 Harmonics 분석을 보면 첫 번째 사진의 Inflator는 좀 더 명확한 배음을 가지고 있고, 두 번쨰 사진의 Limiter는 배음이 두드러지지 않는 대신 전 대역에 걸친 THD가 보인다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Inf_harm.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_harm.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_Inf_harm.png){: .align-center}  

또한 Dynamics 분석을 통해 Inflator는 시간-독립적인 static이지만 Limiter는 release가 존재하는 시간-종속적인 dynamic 프로세스임을 알 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Inf_dyn.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_dyn.png){: .align-center}  

마지막으로 panning을 주어 스테레로 차이를 만들어 준 결과 enhence에는 체널 간 영향이 존재하여 Harminics에서 단순히 gain 차이에 의해 발생할 수 없는 harmonic pattern이 발견되었고, Dynamics 분석을 통해 채널 간 간섭의 경우 어택이 존재함을 알 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_st_har_a.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_st_har_b.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-10-21/Lin-Inf/PD_Lim_st_dyn.png){: .align-center}  

## Outro  

이로부터 우리는 Oxford Dynamics에 있는 warmth 섹션은 Oxford Inflator와 같고, Oxford Limiter에 있는 enhence 섹션은 단순한 waveshaper가 아닌 Look-ahead, time-dependent한 알고리즘임을 알았다.  

이후, Oxford