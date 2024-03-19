---
title:   "OBS 단독으로 리버브 적용하기"
excerpt: "오인페, 마이크, 플러그인, 세팅에 대한 개론"
date:  2024-03-14 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
--- 

## 개요  

이 내용은 OBS만 사용하여 마이크에 리버브를 적용하는 방법을 정리한 것입니다.  

## 1. OBS에서 트랙을 두 개 만들기  

우선 마이크 입력을 받는 트랙을 두 개 만듭니다.  
오인페를 쓰신다면 OBS ASIO [링크](https://github.com/Andersama/obs-asio/releases/latest)를 사용해서 마이크 입력을 받는게 레이턴시(=딜레이)를 적게 받을 수 있습니다.  
관련 내용은 다음 [링크](https://kiriki-liszt.github.io/yg331/production/why-use-OBS-ASIO/)에 정리해두었습니다.  
우선은 일반 오디오 입력 캡쳐로 진행하겠습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/001.png){: width="870px "}{: .align-center .half-width}  

새 오디오 입력 캡쳐 트랙을 하나 추가해줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/002.png){: width="726px "}{: .align-center .half-width}  

이름은 쉽게 파악할 수 있도록 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/003.png){: width="1438px "}{: .align-center .half-width}  

입력 장치는 메인으로 사용할 마이크를 지정해줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/004.png){: width="1928px "}{: .align-center .half-width}  

이와 같이 두 트랙에서 같은 소리가 올라오는 것을 확인합니다.  

## 2. VST 플러그인으로 리버브 걸기  

이제 해당 트랙의 필터를 추가하겠습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/005.png){: width="932px "}{: .align-center .half-width}  

다음과 같이 해당 트랙을 우클릭하여 필터 탭에 들어갑니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/006.png){: width="828px "}{: .align-center .half-width}  

이제 아래의 ' + ' 아이콘을 눌러 VST 2.x 플러그인을 추가해 줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/007.png){: width="1122px "}{: .align-center .half-width}  

쉽게 알아보기 위해 이름을 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/008.png){: width="1722px "}{: .align-center .half-width}  

취향에 따라 적당한 리버브를 골라 추가해줍니다.  

이때 사용 가능한 것은 VST 2 플러그인입니다.  
설치한 리버브 플러그인이 목록에 없다면 설치 시 옵션에서 VST 2 설치에 체크하지 않았거나, 해당 플러그인이 VST 2를 지원하지 않는 것입니다.  
VST 3 버전의 리버브를 사용하고 싶다면 하단의 부록을 참조하시기 바랍니다.  

### 2.1. 리버브의 MIX는 꼭 wet 100%

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/009.png){: width="1232px "}{: .align-center .half-width}  

플러그인에 따라 MIX가 50%에 가 있는 경우도 있습니다.  
하지만 이 세팅은 마이크를 두 트랙으로 사용하기 때문에 꼭 100%로 맞춰서 리버브 트랙에서 리버브'만' 들리게 합니다.  

## 3. 리버브 조절하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/010.png){: width="1086px "}{: .align-center .half-width}  

이제 OBS의 기본 화면에서 리버브의 볼륨을 조정하고, 스피커 아이콘을 클릭해 리버브를 켜고 끌 수 있습니다.  

## 부록  

리버브에 대한 간단한 설명  
<https://kiriki-liszt.github.io/yg331/production/how-to-setup-reverb-simple/>  

소리 좋은 무료 리버브 : Komplete start bundle - RAUM  
[https://www.native-instruments.com/en/products/komplete/bundles/komplete-start/](https://www.native-instruments.com/en/products/komplete/bundles/komplete-start/){: overflow-wrap="anywhere"}  
설치 방법 - <https://thenotemusic.tistory.com/1021>  

Native Instruments VST 설치 위치 설정해야 OBS에서 사용 가능합니다!  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/011.png){: .align-center .half-width}  

Native Access의 Preference에 가서 File Management - VST location (64bit)을 OBS가 인식할 수 있는 위치인
'C:/Program Files/Steinberg/Vstplugins'
로 설정해준 뒤, 설치해야 합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/012.png){: .align-center .half-width}  

주의사항 - 윈도우 사용자명이 한글이 있을 경우 에러가 납니다.  
윈도우 계정명을 영어로 바꾸는 방법은 다음 블로그레 잘 소개되어 있다.  
<https://blog.naver.com/PostView.naver?blogId=rkdalstj7504&logNo=222173490548>  
혹은, 설치를 위해 윈도우 계정을 영어로 하나 만들어서 설치하시기 바랍니다.  

추천 무료 플러그인 모음  
[https://chzzk.naver.com/c02b3049bcb08859d15ca73246bce762/community/detail/10712438](https://chzzk.naver.com/c02b3049bcb08859d15ca73246bce762/community/detail/10712438){: overflow-wrap="anywhere"}  

VST 3 플러그인을 OBS에서 쓰려면 Waves Audio의 StudioRack을 사용하면 됩니다.  
<https://www.waves.com/support/how-to-get-studiorack>  
해당 링크에서 Option 1으로 진행.  
