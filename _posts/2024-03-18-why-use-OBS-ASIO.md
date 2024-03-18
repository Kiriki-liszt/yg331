---
title:   "OBS에서 마이크 입력으로 OBS-ASIO를 권장하는 이유"
excerpt: "기본 '오디오 입력 캡쳐'는 'ASIO 입력 캡쳐'보다 레이턴시가 많습니다"
date:  2024-03-18 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
--- 

## 개요  

이 내용은 '오디오 입력 캡쳐'과 'ASIO 입력 캡쳐'의 레이턴시[^1]를 비교해보았습니다.  

## ASIO란  

ASIO란 Steinberg에서 만든 표준으로 윈도우 환경에서 오디오 인터페이스를 사용하게 해주는 통신 규약입니다.  
이는 윈도우에 내장되어 있는 오디오 통신 규약보다 더 빠르고, 안정적으로 동작하기 위해 만들어졌습니다.  
전부라도 해도 좋을 만큼 DAW의 기본 입출력은 ASIO를 사용합니다.  

## OBS-ASIO란  

이는 OBS에서도 윈도우 내장 오디오 입력이 아닌 ASIO 입력을 사용하게 해주는 기능입니다.  
오인페를 쓰는 경우에만 사용 가능하며, OBS ASIO [링크](https://github.com/Andersama/obs-asio/releases/latest)를 다운로드하여 설치할 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-18/001.png){: .align-center .half-width}  

OBS에서 해당 소스를 선택하여 사용할 수 있습니다.  

해당 트랙의 설정을 열면 다음과 같이 설정할 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-18/002.png){: .align-center .half-width}  

Device로 오인페를 선택할 수 있습니다.  
Format으로 스테레오/모노를 설정할 수 있으며, 마이크 입력의 경우 모노로 두는 것을 추천합니다.  
Channel을 선택하여 오인페의 어떤 입력을 사용할 지 설정합니다.  
이때, 스테레오로 설정할 경우 1번이 왼쪽, 2번이 오른쪽입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-18/003.png){: .align-center .half-width}  

모노인 경우 자동으로 양쪽 다 같이 들어갑니다.  

## 기본 마이크 입력 캡쳐와의 비교  

OBS에서 미디어 재생기로 Dirac Impulse를 재생하고, 오인페에서 케이블로 출력을 입력으로 이어주었습니다.  
아날로그 입력의 차이를 확인하기 위해 오인페의 자체 루프백 기능은 사용하지 않았습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-18/004.jpeg){: .align-center .half-width}  

다음과 같이 녹화를 진행하였습니다.  
버퍼 사이즈는 128 samples입니다.  
OBS 자체 입력 캡쳐는 왼쪽, OBS-ASIO는 오른쪽으로 이어주었습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-18/005.png){: .align-center .half-width}  

이를 큐베이스에서 불러와본 경우, 다음과 같이 둘 사이에 레이턴시가 있음을 확인할 수 있습니다.  

동일 세팅에서 두 번 녹화를 진행한 결과, 둘 다 33ms의 레이턴시 차이를 기록하였습니다.  
이 경우, OBS -> 출력까지는 동일하므로, 순전히 입력 -> OBS에서의 레이턴시 차이라고 할 수 있습니다.  

## 결론  

그러므로 OBS 기본 기능인 '오디오 입력 캡쳐'를 사용하지 않고, 'ASIO 입력 캡쳐'를 사용하는 것이 본인 목소리 모니터링 시 딜레이를 줄일 수 있겠습니다.  

[^1]: 일반적으로 말하는 '소리 지연'은 '레이턴시'가 맞는 표현입니다. '딜레이'라는 용어는 믹싱에서 사용하는 '정해잔 시간 간격마다 소리를 반복 재생하는 효과'입니다. 또한, 이는 '노래방 에코'라고 부르지만, '딜레이'가 맞습니다.  
