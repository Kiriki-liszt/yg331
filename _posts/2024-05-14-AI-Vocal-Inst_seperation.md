---
title:   "AI를 사용해서 보컬과 Inst를 분리해보자"
excerpt: "믹싱 준비"
date:  2024-05-14 00:12:05 +0900

categories:
  - DAW

tags:
  - PC
--- 

## 개요  

AI를 사용해 음원의 Vocal과 Inst(MR)을 분리해보자.  

이 방법은 AI 알고리즘(MDX23)을 사용해 음원의 보컬과 Inst를 분리하는 방법이다.  
이때, 구글의 Colab을 사용해 내 컴퓨터가 아닌 성능 좋은 구글의 가상 컴퓨터로 작동하는 방법이다.  

## 1. MDX23 AI 알고리즘을 구동하는 Colab 페이지 접속  

[https://colab.research.google.com/github/jarredou/MVSEP-MDX23-Colab_v2/blob/v2.5/MVSep-MDX23-Colab.ipynb](https://colab.research.google.com/github/jarredou/MVSEP-MDX23-Colab_v2/blob/v2.5/MVSep-MDX23-Colab.ipynb)

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/01.png){: .align-center .half-width}  

## 2. Installation 진행

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/02.png){: .align-center .half-width}  

Installation 왼쪽의 실행 버튼을 눌러 Colab 가상 컴퓨터와 연결하고, 여기에 AI 알고리즘에 필요한 모델과 구글 계정과의 연동 등을 진행한다.  
이를 통해 구글 계정과 연결시켜 사용할 음원과 분리된 음원을 구글 드라이브에서 사용할 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/02.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/03.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/04.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/05.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/06.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/07.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/08.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/09.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/010.png){: .align-center .half-width}  

## 3. Separation 설정하기  

Separation 탭에서 설정을 입력한다.  

우선, 사용할 음원의 경로를 입력한다.  
이는 좌측의 폴더 아이콘을 눌러 전체 폴더 구조를 볼 수 있으므로, 여기에서 파일을 찾아가 좌클릭 -> 파일 경로 복사하여 쉽게 복붙할 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/011.png){: .align-center .half-width}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/012.png){: .align-center .half-width}  

다음으로 출력 파일의 경로를 입력한다.  
기본은 구글 드라이브에 'output' 폴더가 생겨 그 안에 저장된다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/013.png){: .align-center .half-width}  

취향에 따라 음원 제거 파일 전용 폴더를 만들고,  
그 안에 input과 output 폴더를 만들어 사용할 음원과 분리된 음원을 정리하면 더 좋다.  

output_format은 분리한 음원의 파일 형식으로, 셋 다 상관 없지만 개인적인 취향으로 Float를 사용한다.  
filter_vocals_below_50hz 옵션을 켜면 보컬에서 사용하지 않았을 50Hz 영역을 제거하여 더 깔끔한 보컬과 저음이 조금 더 살아있는 Inst를 얻을 수 있다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/014.png){: .align-center .half-width}  

Model config는 AI의 세부 설정을 조정하는 곳이다.  
위쪽에 About settings에 설명이 적혀 있어 참고할 수 있다.  
보면 알 수 있지만, 이러한 세팅값은 어떠한 경향성을 가지는지 알 수 없으며, 곡바곡으로 다 다르다.  
최상의 퀄리티를 위해서라면 다양항 조합의 세팅을 다 실험해보고 그 결과물끼리 비교해보는게 맞지만,  
대부분의 경우 그 차이는 미묘하기 때문에 기본값 혹은 약간 건드린 정도로 사용하면 충분하다.  

이 또한 마찬가지로, 취향에 따라 BigShifts = 8, weight_VitLarge = 2로 올려준다.  
만약 이 결과가 썩 마음에 들지 않는다면, InstHQ까지는 시도해봐도 좋다.  

## 4. Separation 실행하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/015.png){: .align-center .half-width}  

Separation 왼쪽의 실행버튼을 눌러 시작한다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-05-14/016.png){: .align-center .half-width}  

대략 10분정도 기다리면 맨 아래에 완료 메시지를 띄우며 구글 드라이브에 저장되어 있다.  
이를 다운받아 원하는 대로 사용하면 된다.  
