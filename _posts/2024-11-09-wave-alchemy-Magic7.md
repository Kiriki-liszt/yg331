---
title:   "새로운 무료 리버브 플러그인 - Magic7"
excerpt: "리버브"
date:  2024-11-09 00:19:05 +0900

categories:
  - VST plugin

tags:
  - Reverb
--- 

## wave alchemy - Magic7  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7_Banner4.jpg){: .align-center}  

[https://www.wavealchemy.co.uk/product/magic7/](https://www.wavealchemy.co.uk/product/magic7/)  

11월 8일 wave alchemy사의 새로운 리버브 플러그인인 Magic7이 무료로 출시되었습니다.  
이는 Bricasti M7 하드웨어 리버브에 기반한 플러그인으로, 사실적이고 자연스러운 리버브를 재현합니다.  
이러한 특징으로 피아노와 관현악 등 클래식에 강하지만, 자연스러운 공간감을 강조하기 원하는 보컬에도 아주 적합합니다.  

### 설치하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-free-download.png){: .align-center}  

해당 홈페이지에 회원가입 후, 상기 링크에서 우측의 Download를 선택하면 주문 페이지로 넘어갑니다.  
이때 금액이 자동으로 0원으로 설정되므로 기타 정보를 채워넣고 주문을 완료합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-download-here.png){: .align-center}  

이후 상단의 Accounts -> Downloads 페이지에서 각 운영체제에 맞는 설치파일을 다운로드 받을 수 있습니다.  

## 기능 설명

### 프로그램, 프로그램 그룹  

실제 하드웨어와 동일하게 프로그램과 프로그램 그룹 구조를 가지고 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-program.png){: .align-center}  

프로그램은 Amsterdam Hall, Berliner Hall 등 실제 환경을 주로 담은 특정 환경을 재현하는 리버브 프리셋입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-program-group.png){: .align-center}  

프로그램 그룹은 Ambience, Chambers, Halls, Plate 등으로 크게 보아 동일한 성격을 가진 프로그램들을 카테고리화 한 것입니다.  

### pre-delay, low, air, ensemble/flux  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-lower-params.png){: .align-center}  

이는 리버브의 세부 특성을 조절하는 파라미터들입니다.  

pre-delay는 직접음과 반사음 사이의 시간 차이를 말합니다.  
즉, 큰 공간은 소리가 벽에 부딛혀 귀에 돌아올 때 가지의 시간 차가 크기 때문에 pre-delay가 클 것이고, 좁은 곳은 반대로 pre-delay가 작을 것입니다.  
시작점은 20ms 정도로 두고, 들어보며 조절합시다.  

low와 air는 리버브의 톤을 조절합니다.  
자연스럽고 MR과 자연스럽게 녹아들기 위해서는 air를 줄이고, 샤 하게 보컬을 꾸며주기 원한다면 키워줍니다.  
low는 저음의 공간 울림을 제어하는 것으로, 특수한 목적을 가진 것이 아니라면 주로 줄이는 편입니다.  

ensemble과 flux는 이름을 클릭해 둘 중 하나를 선택할 수 있습니다.  
ensemble은 잔향에 코러스 효과(작은 규모의 다양한 랜덤성)를 적용해 더 풍성하고 화사한 효과를 얻을 수 있습니다.  
flux는 잔향에 큰 규모의 일정한 움직임을 더해 정적이고 딱딱한 인상을 지우기 위해 사용합니다.  
이는 취향의 차이로, 들어보고 세팅해봅시다.  

### smooth, duck  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-right-params.png){: .align-center}  

이는 입력 신호의 특성에 맞추어 리버브를 조작하는 파라미터입니다.  
smooth는 소리의 타격음 부분을 부드럽게 줄여 리버브가 튀지 않고 부드럽게 만들어줍니다.  
duck은 입력 신호의 크기에 맞추어 리버브를 자동으로 줄여 주는 것으로, 과도한 리버브에 보컬이 묻히거나 흐려지는 걸 방지하면서도 긴 잔향을 원할 때 사용합니다.  

### mix  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-mix.png){: .align-center}  

어떻게 보면 제일 중요한 파라미터로, Dry 신호와 Wet 신호의 비율을 조절하는 부분입니다.  
거의 대부분의 경우 리버브를 insert가 아닌 send-return 으로 사용하기 때문에 mix는 100%로 고정합니다.  

### 프리셋  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-preset.png){: .align-center}  

플러그인의 제일 상단에는 프리셋을 선택하거나, 내가 만든 세팅을 프리셋으로 저장할 수 있습니다.  
기본 프리셋들을 사용해도 좋고, 하나하나 만든 세팅을 몇 개 저장해두고 사용하는 것도 좋습니다.  

## 플러그인 내부의 프로그램끼리 비교하기  

드럼이나 기타 등의 경우 room, ambience 등을 주로 사용하겠지만, 여기서는 보컬의 예시를 들어 주로 사용되는 Hall, Plate, Chambers 세 가지의 성향을 비교해보겠습니다.  

### No Reverb  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_No_Reverb.mp3" type="audio/mp3">
</audio>

### Hall - Amsterdam Hall  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-Hall.png){: .align-center}  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_Magic7_-_Hall.mp3" type="audio/mp3">
</audio>

### Plate - Vocal Plate B  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-Plate.png){: .align-center}  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_Magic7_-_Plate.mp3" type="audio/mp3">
</audio>

### Chambers - Sunset Chamber  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-11-09/Magic7-Chamber.png){: .align-center}  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_Magic7_-_Chamber.mp3" type="audio/mp3">
</audio>

## 다른 플러그인과 비교하기  

Magic7은 Hall - Amsterdam Hall 세팅으로 두고, 다른 플러그인들과 비교해보겠습니다.  

### Magic7 - Amsterdam Hall  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_Magic7_-_Hall.mp3" type="audio/mp3">
</audio>

### ReLab LX480 - Random Hall  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_LX480.mp3" type="audio/mp3">
</audio>

### LiquidSonics Seventh Heaven - Large Hall  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_Seventh_Heaven.mp3" type="audio/mp3">
</audio>

### PSP Audio 2445 - Plate  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_2445.mp3" type="audio/mp3">
</audio>

#### Voxengo OldSkoolVerb - Warm Hall  

<audio controls="" name="media">
    <source src="/yg331/assets/audio/2024-11-09/Reverb_Compare_-_OldSkoolVerb.mp3" type="audio/mp3">
</audio>
