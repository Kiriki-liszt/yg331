---
title:   "OBS 단독으로 리버브 적용하기"
excerpt: "오인페, 마이크, 플러그인, 세팅에 대한 개론"
date:  2024-03-12 00:12:05 +0900

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
우선은 일반 오디오 입력 캡쳐로 진행하겠습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/001.png){: .align-center}  

새 오디오 입력 캡쳐 트랙을 하나 추가해줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/002.png){: .align-center}  

이름은 쉽게 파악할 수 있도록 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/003.png){: .align-center}  

입력 장치는 메인으로 사용할 마이크를 지정해줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/004.png){: .align-center}  

이와 같이 두 트랙에서 같은 소리가 올라오는 것을 확인합니다.  

## 2. VST 플러그인으로 리버브 걸기  

이제 해당 트랙의 필터를 추가하겠습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/005.png){: .align-center}  

다음과 같이 해당 트랙을 우클릭하여 필터 탭에 들어갑니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/006.png){: .align-center}  

이제 아래의 ' + ' 아이콘을 눌러 VST 2.x 플러그인을 추가해 줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/007.png){: .align-center}  

쉽게 알아보기 위해 이름을 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/008.png){: .align-center}  

취향에 따라 적당한 리버브를 골라 추가해줍니다.  
이때 VST 3 버전은 지원되지 않기 때문에 VST 2 버전임을 꼭 확인합니다.  
애초에 버전이 안 맞으면 목록에 안 뜹니다.  

### 2.1. 리버브의 MIX는 꼭 wet 100%

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/009.png){: .align-center}  

플러그인에 따라 MIX가 50%에 가 있는 경우도 있습니다.  
하지만 이 세팅은 마이크를 두 트랙으로 사용하기 때문에 꼭 100%로 맞춰서 리버브 트랙에서 리버브'만' 들리게 합니다.  

## 3. 리버브 조절하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-14/010.png){: .align-center}  

이제 OBS의 기본 화면에서 리버브의 볼륨을 조정하고, 스피커 아이콘을 클릭해 리버브를 켜고 끌 수 있습니다.  

## 부록  

소리 좋은 무료 리버브 : Komplete start bundle - RAUM  
<https://www.native-instruments.com/en/products/komplete/bundles/komplete-start/>  
설치 방법 - <https://thenotemusic.tistory.com/1021>  

추천 무료 플러그인 모음  
<https://chzzk.naver.com/c02b3049bcb08859d15ca73246bce762/community/detail/10712438>

VST 3 플러그인을 OBS에서 쓰려면 Waves Audio의 StudioRack을 사용하면 됩니다.  
<https://www.waves.com/support/how-to-get-studiorack>  
해당 링크에서 Option 1으로 진행.  
