---
title:   "LA-2A 컴프레서와 관련된 작은 사실들"
excerpt: "LA-2A의 어랙과 릴리즈, Ratio에 관한 이야기"
date:  2022-08-07 13:12:05 +0900

categories:
  - VST

tags:
  - microphone
  - VST
  - noise
---

보컬에 컴프레션이 필요할 때 가장 먼저 생각나는 컴프레서가 두 개 있다면 그건 아마 LA-2A와 1176일 것이다.  
나도 처음 믹싱을 배울 때 가장 먼저 접했던 컴프레서들이고, 매뉴얼에 쓰여진 특성들을 읽어보고 이해했다 생각했다. 하지만 몇 년 동안 컴프레서들과 싸우다 보니 점점 알게 되는 것들이 늘어나고 다시 매뉴얼을 보니 뒤늦게 깨닫는 것들이 있었다.  
이 포스트는 둘 중 LA-2A 컴프레서에 대해 정리해보려 한다.  

## LA-2A  

![waves LA-2A]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-07-la-2a-little-tips/WAVES LA2A.png){: .align-center}  

이 컴프레서는 다이나믹을 제어하기 위해 광학소자를 사용하고, 컴프레서의 작동 또한 이 소자의 물리적인 특성에 영향을 받는다.  
LA-2A만의 두 특징 중 하나는 바로 입력에 따라 어택과 릴리즈가 달라진다는 것이다.  

우선 한가지 – LA-2A는 입력 신호의 주파수(음역대)에 따라 작동점(Threshold)과 비율(Ratio)이 다르다. 

![LA-2A in-out graph]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-07-la-2a-little-tips/LA2A comp ratio.png){: .align-center}  
![LA-2A in-out graph corrected]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-07-la-2a-little-tips/LA2A comp ratio corrected.png){: .align-center}  

<https://www.uaudio.com/webzine/2004/february/index2.html> 에서 가져온 그래프와 입출력 비율을 맞춘 버전이다.  
이로부터 알 수 있듯이 Soft knee로 작동하고 있으며 Threshold 또한 주파수마다 다르고, 평균적으로 4:1의 Ratio를 가지고 있지만 저음에서는 3.3:1, 고음에서는 대략 5.5:1까지 Ratio가 높아진다.  
이러한 비선형적 반응이 이 LA-2A만의 특징을 나타낸다.  


또 다른 LA-2A의 특징은 입력에 따라 어택과 릴리즈 시간이 달라지는 것이다. 어택 시간은 입력 신호의 주파수에 따라 달라지지만 평균적으로 10ms<sup id="a1">[1](#footnote1)</sup>를 가지지만 릴리즈 시간은 이보다 조금 더 복잡하다.  
릴리즈 시간의 경우 50% 지점까지 60ms를 가지지만 완전한 컴프레션의 종료까지는 1에서 15초까지 길어진다.  
즉 LA-2A의 릴리즈 타임은 서로 다른 두 개의 릴리즈가 복합적으로 나타난다 생각할 수 있다.  
이는 광학 소자의 물리적인 특성 때문에 나타난다.  
또한 이 소자는 컴프레서가 오래 혹은 강하게 걸릴 경우 릴리즈 시간이 늘어난다.  
이러한 입력 신호의 성격에 따라 달라지는 특성을 ‘Program dependent’<sup id="a2">[2](#footnote2)</sup>라고 한다.  

![waves LA-2A]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-07-la-2a-little-tips/WAVES LA2A R37.png){: .align-center}  

두 번째 중요한 특징은 바로 사이드체인 컨트롤 노브, "Emphasis control" 노브라고 부른다.  
설계도상 37번째 저항 소자라서 "R37" 노브라고 부르기도 한다.  
이 노브는 실제 출력에는 관여하지 않고 컴프레서를 작동시키는 신호에만 적용하여 1kHz 이상의 주파수를 부스트하는 EQ이다.  
이를 통해 입력 신호가 고음에 더 민감하게 반응하도록, 저음에 영향을 덜 받게 설정할 수 있다.  
이 노브를 조정하면 너무 찌르는 고음에만 컴프레싱이 걸리도록, 즉 디에서 느낌을 살짝 내면서 청감상 좀 더 부드럽게 할 수 있다.  
실제 하드웨어가 시계방향으로 끝까지 돌렸을 때 0%, 반시계 방향으로 끝까지 돌렸을 때 100% 적용되게 설계되어 있다.  
따라서 플러그인들도 이를 따라 오른쪽을 flat, 왼쪽을 Hi-freq라고 표기한다. 

![LA-2A THD]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-07-la-2a-little-tips/LA-2A THD.png){: .align-center}  

살짝 짚을 부분은 플러그인마다 달라지지만 해당 컴프레서는 통과하는 것만으로도 배음이 걸린다는 것이다.  
이는 해당 하드웨어가 많은 진공관과 트랜스를 통과하기 때문에 걸리는 배음들을 구현해놓은 특성이다.  
간단하게 1kHz 사인파를 입력하고 gain reduction을 0으로 내려도 2, 3, 4, ... kHz 모두 배음이 나타나는 것을 확인할 수 있다.  
따라서 단순히 걸기만 해도 소리가 달라지는 것이 맞다.  
만약 믹싱을 하면서 많은 플러그인이 쌓이면서 새츄레이션이 걸리는게 들린다면 이러한 부분들을 잘 확인하고 이런 아날로그 계열 플러그인을 디지털 계열로 바꾸어야 할수도 있다.  




> <b id="footnote1"><sup>1</sup></b> 간혹 오래된 버전의 LA-2A 매뉴얼을 보면 10 μsec = 10 micro-sec 으로 표기되어 있기도 한다. 하지만 이는 유명한 오타로 현재 생상하고 있는 Universal Audio의 홈페이지를 보면 10 mili-sec으로 나타나 있다. [↩](#a1)  
<b id="footnote2"><sup>2</sup></b> 이 Program Dependent 특성은 다른 컴프레서들에도 나타난다. 이를 다루는 포스팅이 있을 것이다.  [↩](#a2)
