---
title:   "Oversampling 이야기 - Kaiser-Bessel filter"
excerpt: "플러그인 오버샘플링 이야기"
date:  2023-11-26 00:12:06 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## Fir filter  

Finite impulse response filter는 유한한 크기의 impulse response에 기반한 convoluton filter이다.  
이는 필연적으로 tap 수에 비례하는 latency를 발생하고, step response에서 impulse의 앞에 신호가 발생하게 되어 linear phase eq와 같이 pre-ringing이 발생한다.  
하지만 선형 위상응답을 얻을 수 있다는 장점이 있어 oversampling에 사용하면 초고역의 위상을 더럽히지 않을 수 있다.  

## Kaiser-Bessel filter  

J. F. Kaiser가 고안한 Kaiser-Bessel filter는 cutoff frequency에서 foldback이 일어났을 때, 원래이 모습이 그대로 복원된다(이는 수학적으로 증명된 사항은 아니고, 실험적으로 발견된 것이다). "Nonrecursive digital filter design using I0-sinh window function"  
이 필터의 계수는 다음 두 사이트에서 구할 수 있으나, 나는 c++로 작성하여 저 정확한 계수의 유효숫자를 얻었다.  
<https://arc.id.au/FilterDesign.html>  
<https://fiiir.com/>  

그 예시로, x4 오버샘플링과 quater-band fir을 사용했을 때 주파수 응답은 다음과 같다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-26/001.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-26/002.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-26/003.png){: .align-center}  

정말로 아무것도 하지 않은 초기 상태에서 주파수 응답이 flat하다.  
