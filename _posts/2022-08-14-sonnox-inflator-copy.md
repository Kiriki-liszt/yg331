---
title:   "SONNOX Inflator 카피하기"
excerpt: "플러그인 카피해서 만들어보기 - 1"
date:  2022-08-14 00:12:05 +0900

categories:
  - VST
  - saturation

tags:
  - digital
---

처음 이 플러그인을 알게 된 것은 Alan JS Han님의 블로그에서였다.  
정확히 무슨 포스트였는지 기억나지는 않지만 이 플러그인을 사용하고 계신다, 믹스버스에서 약간 걸어준다, 하는 식으로 사용중이신 거로 기억한다.  
이후 유튜브 영상에서 본인의 믹스 버스 템플릿을 공개하셨을 때 있기도 했다.  

그래서 계속 사려고 각을 보다가 오만원 정도에 풀려서 참지 못하고 질러버렸다.  
처음 믹스 버스에 걸었을 때 엄청난 차이가 들렸고, 이후로 이 플러그인의 신봉자가 되었다.  
이후 드럼, 베이스, 기타, 보컬 등에도 하나씩 걸어보며 순식간에 모든 트랙에 존재감이 생기며 소리에 두꼐감이 생기고 힘이 실리고, 등등...
물론 한두 믹스 이후에는 너무 남용한 듯한 소리가 들려 좀 자제하게 되었지만 보컬과 믹스버스에는 한 자리를 차지하고 있다.  

## SONNOX Oxford Inflator  
  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/inflator-V3-gui2.jpg){: .align-center}  

최근 메인으로 쓰는 노트북에 리눅스를 듀얼부팅으로 구성하다가 뭘 잘못 건드렸는지 와이파이 모듈이 자꾸 에러를 뿜으며 잘 붙지 않게 되었다.  
두달간 다섯번정도 C드라이브를 밀고 재설치한 것 같다.  
사실 아직도 좀 불안정해서 절전모드 잘못 들어가거나 하면 어김없이 와이파이가 작동하지 않는다.  

그래서 생긴 문제 중 하나가 바로 플러그인들의 라이센스 문제다.  
특히 iLok 계열 플로그인들은 순간 실수해서 남겨두고 윈도우를 밀면 해당 라이센스를 복수할 수 없게 된다.  
그렇게 프로툴즈 라이센스도 하나 날렸다.  

이후로 윈도우랑 와이파이가 좀 안정될 때 까지는 iLok을 쓰는 플러그인들을 안 쓰려고 했다.  
그런게 이 Inflator가 하필 iLok 라이센스를 쓴다.  

이 문제를 해결하기 위해 몇 가지 시도를 했다.  
첫번째는 이 플러그인의 카피 플러그인을 찾아본 것이다.  
구글링하면서 하루를 통째로 보냈지만 딱히 보이지 않았다.  

그러다 REAPER 커뮤니티에서 재미있는 것을 발견했다.  
inflator의 작동원리를 알아냈고, 카피하는 데 성공했다는 것이다.  

> "음질과 다이나믹의 손해 없이 청감 음량을 올리는 플러그인이다"

그들은 이에 주목하여 이 플러그인이 일종의 waveshaper라고 가정하였다.  
그래서 실제로 이 플러그인을 분석해보았다.  

## 특징 분석  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/inflator default.png){: .align-center}  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/inflator dynamics.png){: .align-center}  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/inflator effect100.png){: .align-center}  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/inflator THD.png){: .align-center}  

가장 기본적인 세팅으로 로딩했을 때의 입출력 그래프이다.  
이로부터 Inflator가 non-linear한, 일종의 saturation 플러그인임을 알 수 있다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/inflator compression.png){: .align-center}  

하지만 이것이 컴프레서는 아니다.  
Threshold를 넘어서는 소리를 일정 비율로 감소시키지 않기 때문이다.  
비교하자면 어택이 0인 soft knee Limiter에 가깝다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator-effect-knob.gif){: .align-center}  

Effect 슬라이더는 일반적인 Mix 기능으로 추정할 수 있다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator-curve-knob.gif){: .align-center}  

Curve 슬라이더는 입출력 non-linearity 특성을 조금 변화시킨다.  
-50으로 갈수록 조금 더 linear해지고, 50으로 갈수록 조금 더 휘어진다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator-wavefolder-1.gif){: .align-center}  

그러나 Inflator의 또다른 특성은 입력이 0dB를 넘어섰을 때 나타난다.  
늘어나던 입력이 다시 줄어들기 시작한다.  
즉 Limiter나 Clipper가 다이나믹을 죽일 때 Inflator는 소리를 크게 키워주면서도 디테일한 다이나믹을 유지한다는 것이다.  
이것이 이해하기 어렵다면 다음과 같이 sine파를 주었을 때 끝부분이 접히는 것을 보면 이해하기 쉽다.  
이 때문에 이 플러그인은 waveshaper이고 그 중 정확히는 wavefolder인 것이다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator-wavefolder-2.gif){: .align-center}  

이러한 특성 때문에 입력미터가 0dB를 조금 넘도록 플러그인이 입력 슬라이더를 조정하였을 때 이 플러그인만의 특성을 제일 돋보이게 사용할 수 있는 것이다.  
청감 레벨은 상승하고, 실제 최대 레벨이 커지지도 않고, 다이나믹을 건드려 그루브감이 변하지도 않는 아주 멋진 일이 벌어지기 시작한다.  

## 알고리즘 확인

다시 REAPER 커뮤니티로 돌아가서, 사람들은 이 입출력 커브를 발견하고 이와 동일한 형태를 가지는 함수를 추정하기 시작했다.  
얼마 지나지 않아 그들은 거의 완벽하게 들어맞는 함수를 찾아냈다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator func 1 e.png){: .align-center}  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator func 2 e.png){: .align-center}  

그리고 원본와 이 카피는 서로를 완벽하게 상쇄한다.  
REAPER에서 두 트랙에 동일한 핑크 노이즈를 주고 하나의 위상을 뒤집으면 둘이 합쳐진 최종 출력은 정말로 없어진다.  
그것도 다양한 세팅값에 대해 모두 성공한다.  

![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator NULL 1.png){: .align-center}  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator NULL 2.png){: .align-center}  
![SONNOX Oxford Inflator({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-14-inflator-1/Inflator NULL 3.png){: .align-center}  

그러므로 이 코드가 원본과 같거나, 매우 작은 차이를 가진다는 것을 확인했다.  

## 플러그인으로 컴파일  

문제는 내가 REAPER DAW를 거의 쓰지 않다는 것이다.  
내 메인 DAW는 큐베이스고, 이미 사서 쓴 지 오래되었기 때문에 손에 익기도 했고 돈 아까워서 바꾸고 싶지 않다.  
따라서 이 JSFX 코드를 VST 형식으로 컴파일해야 한다.  

오랜 검색 끝에 나에게 두 가지 선택지가 주어졌다.  
하나는 이 알고리즘을 C++로 다시 짜고, 큐베이스에서 제공하는 VST3 API에 맞춰서 새로 만드는 것이다.  
그래서 비주얼 스튜디오 커뮤니티를 설치하고 C++ 환경을 구현해주고, API 파일을 다운로드 받아 동봉된 예제들을 컴파일 하는데까지는 성공했다.  
하지만 여기에서 다시 GUI를 추가하는 방법과 그것을 이어주는 방법을 익히기까지 너무 길이 멀어 보였다.  
게다가 나는 쌩 C 코딩을 하는 쪽이지 C++은 한번도 해본 적이 없었다.  
결국 C++기반 프로젝트는 여기까지 하고 고이 접어 두었다.  
나중에 C++을 배운다면 그 후에 다시 시도해보기로 했다.  

또 다른 선택지는 JSFX 언어에서 C++로 크로스 컴파일 하는 것이다.  
다행히도 이와 관련된 자료는 아주 조금이지만 남아있었다.  
동일하게 REAPER 커뮤니티에서 활동하시던 분이 이 JSFX 언어를 위한 IDE를 개발하셨던게 남아있었다.  
Geep Jeez! 라는 이 프로그램은 JSFZ의 코드를 줄 단위로 phasing하여 C++으로 바꾼 다음, gcc 기반으로 컴파일한다.  
이때, 최종 결과물은 .dll 파일로 윈도우즈용 vst 확장자이다.  
그리고 이 API가 사실 좀 문제인게, 정식 API 파일은 steinberg에서 개발하였기 때문에 배포에 제한이 걸려 있다.  
따라서 개발자가 리버스 엔지니어링을 해버렸다...  
그래도 문제는 아직 남아있다.  
문서에 이 API를 리버스 엔지니어링하여 사용하는것도 허가하지 않는다고 명시되어 있었던 것이다.  
이 때문에 개발자분도 어느 순간 사라지셨으며 이를 기반으로 플러그인을 만들고 배포하시던 분들도 사라졌다.  

하지만 인터넷 아카이브에는 아직 해당 프로그램이 남아 있다.  
깃헙에도 해당 프로그램의 원본 코드는 남아 있지만, Pascal이라는 언어로 쓰여 있어서 맞게 컴파일 해야 한다.  
그리고 난 파스칼이라는 언어응 해본 적이 없기 때문에 얌전히 릴리즈된 인스톨러로 설치하고, 권장하는 버전의 gcc를 설치했다.  
시행 착오 끝에 내가 원하는 대로 vst 형식의 dll 파일을 만드는 데 성공하였다!

다음 스텝은 여기에 적절한 GUI를 붙이는 것이다.  
처음에는 지원하는 툴이 있을 줄 알았지만, 그런 건 없었다.  
그래서 GUI를 지원하는 다른 JSFX 플러그인을 찾아서, 내부 코드를 분석한 뒤 이 Inflator 코드에 이식했다.  
처음에는 LOUDER라는 JSFX 플러그인을 참고했으나, 거기에서 사용한 코드로 컴파일한 결과 이미지가 들어있는 별도의 폴더가 필요했다.  
즉 dll 안에 이미지가 들어가지 않고, 같은 폴더 내에 이미지가 존재해야 했다.  
나는 이러한 방식은 원하지 않았고, 다른 개발자의 플러그인을 찾아보았다.  
마침 Sonic Anomaly라는 개발자의 플러그인들이 JSFZ와 dll 두 형식으로 배포하고 있었고, 그 코드를 분석하여 적용한 결과 이미지가 내장된 단일 dll 파일을 컴파일 할 수 있었다.  

## 비슷한 플러그인으로 같은 효과 내기  
