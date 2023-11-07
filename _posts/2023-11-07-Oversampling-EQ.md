---
title:   "Oversampling 이야기 - EQ"
excerpt: "플러그인 오버샘플링 이야기"
date:  2023-11-07 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 왜 EQ를 Oversampling하는가  

VST 플러그인을 만들면서 생기는 문제 중, EQ의 경우 Nyquist 근처에서 주파수 응답과 위상 응답에 Crampling이 발생하는 문제가 있다.  
이를 해결하기 위해 보상 shelf를 더하거나 할 수 있지만, 이는 위상 응답에서의 문제를 해결하지 못한다.  
하지만 Oversampling을 도입한다면 내부 IIR filter가 타겟한 샘플링주파수에서의 응답을 만들어내고, 주파수 응답과 위상 응답 모두 개선할 수 있다.  

또한, EQ에 적용하는 Oversampling은 harmonic content를 생성하지 않아 Aliasing이 발생하지 않는다.  
그러므로 우리는 높은 탭 수를 가지는 필터가 필요하지 않다.  
오히려 적당히 nyquist에서 fold-back하여 flat한 주파수 응답을 가지는 필터가 더 이상적이다.  

## 어떤 EQ가 Oversampling을 사용하는가  

제일 유명한 EQ로는 Massenberg DesignWorks의 MDWEQ가 있다.  
MDWEQ는 신호처리 샘플링주파수를 최소 88.1k/96k로 보장하므로 48k 프로젝트에서 x2 oversampling이 작동한다.  

Fabfilter의 Pro-Q 3 또한 natural phase, linear phase에서 Oversampling으로 동작한다.  

마지막으로 TDR의 Slick EQ 시리즈도 기본 load 상태에서 oversampling이 작동하고 있다.  

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

EQ process는 주로 IIR 필터를 사용해 이루어지는데, 이는 같은 주파수를 타겟으로 필터를 구성하여도 필터가 작동할 샘플링 주파수에 따라 다른 응답을 보인다.  
즉, 48k에서의 15k high shelf 응답과 192k의 15k high shelf 결과가 다르다.  
그러므로 우리는 192k의 15k high shelf 응답을 가지고 24k 대역제한을 시킨 결과를 사용하는 것이다.  
