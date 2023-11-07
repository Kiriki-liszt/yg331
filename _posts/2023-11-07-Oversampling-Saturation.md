---
title:   "Oversampling 이야기 - Saturation"
excerpt: "플러그인 오버샘플링 이야기"
date:  2023-11-07 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 왜 Saturation을 Oversampling하는가  

VST 플러그인을 만들면서 생기는 문제 중, Saturation의 경우 생성된 Harmonic content가 Nyquist에서 fold-back되어 non-harmonic noise가 되는, Aliasing이 발생한다.  
이를 해결하기 위해 Oversampling을 도입한다면 harmonic content가 차지할 수 있는 주파수 스펙트럼이 넓어지므로 효과적으로 Anti-Aliasing이 된다.  

## 어떤 플러그인이 Oversampling을 사용하는가  

Saturation이 발생하는 플러그인 중 Oversampling을 사용하는 플러그인으로는 Universal Audio의 제품들이 있다.  

그 외에도 Fabfilter의 Pro-C, Pro-L 시리즈, iZotope의 제품들, TDR의 kotelnikov, SSL Native 시리즈 등이 있다.  

## 어떻게 작동하는가?  

> 1. input sample  
> 2. upsampling  
> 2.1. zero-fill  
> 2.2. Low pass Filter  
> 3. EQ process  
> 4. downsampling  
> 4.1. Low pass Filter  
> 4.2. Decimation  
> 5. output sample  

Oversampling은 위와 같은 단계를 걸쳐 일어난다.  

Zero-fill 이란 샘플링 주파수를 정수배로 올릴 때에 사용하는 것으로 입력 신호의 스펙트럼이 확장될 때 기존 신호가 nyquist를 중심으로 반전되어 채워지는 방법이다.  
이렇게 생성된 신호는 원 신호가 아닌 것을 가지게 되므로, nyquist 근처에서 low pass filter를 걸어 다시 원 신호의 스펙트럼 대역을 가지도록 한다.  

Decimation 이란 반대로 주파수를 정수대로 감소시킨 때 사용하는 것으로 입력 신호의 스펙트럼이 nyquist를 중심으로 반으로 접혀 중첩되는 것이다.  
이때 nyquistq보다 위에 있던 신호가 aliasing되어 들어오므로 이를 제거하기 위해 decimation 전에 low pass filter로 제한하여야 한다.  

이때 Upsampling 과정에서의 LPF는 입력 신호를 대역제한 하는 것으로 최종 출력에서 낮은 레벨 noise의 clogging을 제어한다.  
Downsampling 과정에서의 LPF는 실질적으로 Aliasing을 제거하는 것으로 높은 레벨의 noise를 제어한다.  
