---
title:   "DAW 없이, OBS 단독으로 컴프레서 적용하기"
excerpt: "오인페, 마이크, 플러그인, 세팅에 대한 개론"
date:  2024-03-25 00:12:05 +0900

categories:
  - Setup

tags:
  - VST
  - PC
--- 

## 개요  

이 내용은 OBS만 사용하여 마이크에 컴프레서를 적용하는 방법을 정리한 것입니다.  

## 1. 컴프레서란?  

컴프레서는 다이나믹스 - 소리의 크기 범위, 조용한 부분과 큰 부분 사이의 크기 차이 - 를 줄이는 장치입니다.  
이를 통해 더 안정적인 마이크 소리를 얻기 위해 사용합니다.  
예를 들어, 노래를 부를 때 하이라이트 부분의 큰 소리가 깨지는 것을 방지하기 위해 사용하실 수 있습니다.  

## 2. 컴프레서 고르기 + 무료 컴프레서 추천  

VST 2.0에 호환 가능하고 쓸만한 무료 컴프레서 몇가지를 골라보자면, TDR Kotelnikov, TDR Molotok, Klanghelm DC1A, Analog Obsession LALA, Analog Obsession Fetish 등이 있습니다.  
Analog Obsession 제품들은 이제 업데이트 되어 VST 2.0 지원이 중단되었지만, 예전 버전의 설치 파일 링크는 살아있으니 다운로드 받아서 사용하실 수 있습니다.  

* LALA : [Mac](https://analogobsession.com/wp-content/uploads/2021/04/LALA_2.1.pkg) / [Win](https://analogobsession.com/wp-content/uploads/2021/04/LALA_2.1.exe)  

* Fetish : [Mac](https://analogobsession.com/wp-content/uploads/2021/06/FETISH_5.0.pkg) / [Win](https://analogobsession.com/wp-content/uploads/2021/06/FETISH_5.0.exe)  

Analog Obsession 말고도 플러그인을 설치할 때, 설치하는 위치를 정확히 지정해주어야 OBS가 인식할 수 있습니다.  

'C:/Program Files/Steinberg/Vstplugins' 경로를 꼭 확인합시다.  

이 외, 윈도우 유저라면 TLS 1295 LEA Compressor, VOS ThrillseekerLA 등도 있습니다.  

세팅이 쉬운 것은 LALA, DC1A가 제일 편합니다.  
LALA의 Peak Reduction, DC1A의 Input을 조절해 컴프레서가 작동하는 세기를 조절하고,  
Gain / Output을 조정해 볼륨을 조절하면 됩니다.  

세팅이 까다롭지만, 그만큼 의도한 작동을 할 수 있는 것은 TDR Kotelnikov입니다.  
사용하실 때는 우상단에 Precise를 Eco로 바꾸시는게 CPU 부담 훨 적어집니다.  
다만, 이 플러그인은 3ms 정도의 딜레이가 발생하므로 실시간 모니터링 시 차이가 느껴지실 수 있습니다.  

나머지 플러그인들은 두 부분의 중간에서 적당한 편리성과 적당한 조작성을 가지고 있습니다.  

만약 '보컬에 대해 실패할 수 없는 컴프레서' 하나를 고르자면 Analog Obsession LALA입니다.  

컴프레서에 대한 설명은 다음 [블로그 링크](https://kiriki-liszt.github.io/yg331/plugin/how-to-setup-compressor-simple/)에 정리해두었습니다.  

## 3. OBS 트랙 만들기  

우선 낮은 레이턴시를 위해 OBS ASIO[(다운로드 페이지)](https://github.com/Andersama/obs-asio/releases/latest)를 사용하는 마이크 트랙을 만듭니다.  
관련 내용은 다음 [블로그 링크](https://kiriki-liszt.github.io/yg331/setup/why-use-OBS-ASIO/)에 정리해두었습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/OBS_0.png){: .align-center .half-width}  

사용에 앞서, 기존에 사용하던 OBS 자체 마이크 입력 캡쳐는 OBS의 설정에 들어가 비활성화 처리하여 꺼줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/OBS_1.png){: .align-center .half-width}  

이제 ASIO 입력 캡쳐 트랙을 하나 추가해줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/OBS_2.png){: .align-center .half-width}  

이름은 쉽게 파악할 수 있도록 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-18/003.png){: .align-center .half-width}  

Device로 사용하는 오인페를 선택합니다.  
Format은 리버브와 다르게 모노로 설정합니다.  
Channel에 오인페 입력 중 어느쪽인지 설정합니다.  
대부분의 오인페 마이크 입력은 1번이 기본입니다.  

## 4. 컴프레서 적용하고 세팅하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/OBS_3.png){: .align-center .half-width}  

만든 트랙의 필터에 들어가 VST 2.x를 하나 추가합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/OBS_4.png){: .align-center .half-width}  

해당 필터에서 사용하고자 하는 컴프레서를 하나 불러옵니다.  
이번 예시에서는 LALA를 사용하는 법과, Kotelvnikov를 사용하는 법 하나씩 해보겠습니다.  
'플러그인 인터페이스 열기'를 눌러 선택한 플러그인의 GUI를 볼 수 있습니다.  

### LALA  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/LALA_setting.png){: .align-center .half-width}  

위과 같이 세팅하는 것을 기본으로 시작합니다.  
이때 Gain Reduction을 잘 확인해야 합니다.  
이 값을 조정해 노래하거나 말할 때, 평상시에는 1~2 dB 정도만 걸리도록 합니다.  
그리고 큰 소리를 낼 때와 노래의 큰 부분을 부를 때, 5~7dB 정도 걸리도록 합니다.  

### Kotelnikov  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-25/Kotelnikov_setting.png){: .align-center .half-width}  

이 경우, 처음부터 'Vocal Bus Tight' 프리셋을 불러오는 것을 추천합니다.  
이도 마찬가지로 Threshold를 조정해 노래하거나 말할 때, 평상시에는 1~2 dB 정도만 / 큰 소리를 낼 때와 노래의 큰 부분을 부를 때, 5~7dB 정도 걸리도록 합니다.  
그리고 우상단의 Precise를 Eco로 변경해줍니다.  

## 5. 녹화해서 스스로 들어보기  

제일 중요한 부분입니다.  
이렇게 세팅을 하고, OBS 녹화를 통해 어떻게 들리는지 피드백을 진행해봅니다.  
컴프레서를 통과한 소리는 답답해지기 쉽기 때문입니다.  
이는 EQ사용해 컴프레서 전에 저음을 살짝 줄이거나, 컴프레서 이후에 고음을 조금 올려볼 수 있습니다.  

녹화할 때, 평소보다 목소리가 작게 나올 가능성이 있습니다.  
의식적으로 목소리를 좀 더 키워서 녹화해보거나, 실제 방송을 해보고 피드백을 들어보는 것도 좋습니다.  

## 부록  

상기한 것 이외에, VST 3 플러그인을 OBS에서 쓰려면 Waves Audio의 StudioRack을 사용하면 됩니다.  
<https://www.waves.com/support/how-to-get-studiorack>  
해당 링크에서 Option 1으로 진행.  
