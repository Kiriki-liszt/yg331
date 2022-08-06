---
title:   "[VST] 플러그인에 따라 발생하는 딜레이 차이"
excerpt: "REAPER를 사용해서 플러그인마다 걸리는 샘플 확인"
date:  2021-06-02 19:19:47

classes: wide

header:
  teaser: # "https://farm5.staticflickr.com/4076/4940499208_b79b77fb0a_z.jpg"
  video:
    id: # -PVofD2A9t8
    provider: # youtube

categories:
  - 플러그인

tags:
  - REAPER
  - 플러그인
  - sample delay compensation


# YYYY-MM-DD HH:MM:SS +/-TTTT 
# hours, minutes, seconds, and timezone offset are optional.

# last_modified_at: 2019-04-13T08:06:00-05:00

---

얼마 전에 라이브용으로 iZotope 시리즈를 추천했다가 딜레이 때문에 민망했던 상황이 있었습니다. 평상시에 아무 문제 없이 레코딩도 하고 그랬던거 같은데 은근 문제가 심각하더라고요...? 그래서 REAPER를 사용해서 각 플러그인들에 의해서 발생하는 딜레이들을 체크해보았습니다.


REAPER에는 View - Performance Meter가 있어서 각 트랙이 사용하는 CPU와 PDC : Plugin Delay Compensation을 확인할 수 있습니다. PDC는 플러그인에 의해서 발생하는 딜레이를 샘플링 개수로 받아서 모든 나머지 트랙에 걸어버려 싱크를 맞춘다는 개념입니다. 다른 DAW들도 모두 사용하고 있는 기능이지만 이를 REAPER에서는 확인할 수 있게 열어준 것입니다. 


대부분의 경우 이 PDC 값은 플러그인 제조사에 의해 제공되지만 아주 가끔씩 값이 없거나, 각자의 상황에 조금씩 다르게 나타날 수 있습니다. ㄹㅇ로 혹시 모르니까 체크해봅니다. 테스트해보니까 아직까지는 다 똑같이 나왔습니다. LALA라는 LA-2A 복각은 0 samples가 아니라 1 samples가 뜨기는 했는데 0.02ms는 사람이 구분할 수 없죠...


TBProAudio에서 개발한 ABLevelMatchingJSFX를 사용하면 본인이 직접 플러그인 레이턴시를 측정할 수 있습니다. 테스트해볼 플러그인들 가장 앞뒤로 걸어주고 맨 앞에서 신호 시그널을 쏘면 가장 끝에서 받은 타이밍으로부터 역산하는거죠. 이로부터 플러그인이 레이턴시를 만들어내는지 아닌지를 알 수 있습니다. 


확인해서 나오는 값은 samples로 주어지는데, 이거는 사용하시는 오디오의 샘플링레이트랑 관계있는 값입니다. 샘플링레이트가 samples/sec 즉 1초를 얼마나 잘게 쪼갤 것인지를 말하므로 예를 들면 딜레이가 256 samples로 나올 때 44.1kHz 상황에서는 256/44100=0.0058sec=5.8ms 대략 6밀리초만큼 밀려서 들리는겁니다. 


레이턴시가 나온다면 타이밍이 중요한 노래 방송에는 사용하기 힘든 플러그인이라 보시면 되겠습니다. 물론 최종 출력 MIX BUS에 걸어버리면 트랙들 간에 딜레이 신경 안 써도 되니까 사용해도 되겠죠. 아니면 모든 트랙에 똑같이 걸어버릴 수도 있겠으나 그러면 본인 목소리 모니터링 시 딜레이가 발생하니까 그냥그냥 하네요. 이건 각자 세팅에 따라 봐 가면서 사용하시면 될 것 같습니다. 

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2021-06-02-vst-plugin-delay/8cb17843a1ff41e658877e4ff7360f8a.png){:  width="50%" .align-center}  

테스트해본 (무료)플러그인들 – iZotope는 최근 한 달간 무료로 풀린 적이 많아서 넣어봤습니다. 
  
  
|      제조사      	|     이름     	| samples 	|                                          비고                                         	|
|:----------------:	|:------------:	|:-------:	|:-------------------------------------------------------------------------------------:	|
|        OBS       	|    RNNoise   	|    0    	| OBS에서 사용하는 잡음 제거의 VST 버전                                                 	|
|      Reaper      	|    ReaFir    	|  y=f(x) 	| 세팅에 따라 다름 : FFT 사이즈에 일대일로 비례합니다.                                  	|
|      Reaper      	|    ReaGate   	|  y=f(x) 	| 세팅에 따라 다름 : Pre Open을 건드리지 않는다면 0 samples이고 이외의 경우 발생합니다. 	|
|      iZotope     	|   Nectar 3   	|   3247  	| Elements                                                                              	|
|      iZotope     	|     RX 7     	|    0    	| Elements                                                                              	|
|      iZotope     	|   Neutron 3  	|    0    	| Elements                                                                              	|
|      iZotope     	|    Ozone 9   	|   784   	| Elements                                                                              	|
| Analog Obsession 	|   BUSTERse   	|    0    	|                                                                                       	|
| Analog Obsession 	|     LALA     	|    1    	|                                                                                       	|
| Analog Obsession 	|    LOADED    	|    0    	|                                                                                       	|
|  Tin Brook Tales 	| TLS 1295 LEA 	|    0    	|                                                                                       	|
|        D16       	|   Frontier   	|   176   	|                                                                                       	|
|   Thomas Mundt   	|    LoudMax   	|    66   	| ISP ON                                                                                	|
|        TDR       	|  Kotelnikov  	|   184   	|                                                                                       	|
|        TDR       	|  VOS SlickEQ 	|   183   	|                                                                                       	|
|   Denis Tihanov  	|   OrilRiver  	|    0    	|                                                                                       	|
|       GVST       	|     GSnap    	|   481   	|                                                                                       	| 



iZotope의 경우 RX 시리즈는 딜레이가 없지만 이외의 경우 상당한 딜레이가 포함됩니다. 

ReaFir가 가장 의외의 경우였는데요, FFT를 기본적으로 4096으로 잡아서 처리합니다. 이 FFT가 어느 주기로, 어떤 음질로 소리를 처리할거냐 하는 의미입니다. 높게 잡으면 음질은 좋아지지만 처리하는 주기가 길어지고 짧게 잡으면 빨리빨리 처리하지만 음질은 버리는거죠. 디폴트값인 4096의 경우 약 93ms만큼 딜레이가 생깁니다. 이정도면 Slapback 딜레이정도는 되죠. 

역시 진리의 iZotope RX Voice de-noise... 비싼 값을 하네요...

가끔 60Hz AC전원 노이즈나 1kHz의 배수로 나타나는 USB 통신 노이즈가 올라온다면 De-hum도 정말 좋습니다. 



결론 ) 노래방송을 하실 때 이 ReaFir을 사용하시는건 까다로울 것 같습니다.

사용해야 한다 가정한다면 Audio Monitor 라는 OBS 확장 플러그인으로 본인 목소리를 저 ReaFir 통과하기 전에 미리 이어폰으로 빼내서 모니터링하시고 고급 오디오 설정에서 해당 트랙에 –93ms 오프셋을 주어야 가능하지 싶습니다. 물론 이때 저 Audio Monitor가 얼마나 딜레이를 만들지 알 수가 없어서 가능할지는 모르겠습니다.

그냥 저챗 하실때는 뭐, 딜레이 신경 안 쓰셔도 되죠.



LoodMax랑 D16 Frontier, Ozone같은 맥시마이저 계열도 은근 레이턴시가 있었네요. 아마 Look-Ahead 기능 때문에 그런 것 같습니다. MIX BUS에는 좋은데 개별 트랙에 사용할 때는 주의하셔야 할 것 같습니다. 의외로 TDR 플러그인들도 딜레이가 있었습니다. 



ReaStream 딜레이 테스트 - 1

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2021-06-02-vst-plugin-delay/e29e43b8c7bf0e074c19c1e06042c5ce.png){: .align-center}  


가끔 OBS랑 다른 프로그램끼리 연결하거나 할 때 가끔 사용되는 플러그인입니다. REAPER  내부에서 트랙끼리 보내는 상황입니다. 512 samples, 12ms 정도 나타납니다.



ReaStream 딜레이 테스트 – 2


![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2021-06-02-vst-plugin-delay/5c49e04ef4b1201eb06b2ddcc4e2e179.png){: .align-center}  

실제로 프로그램 사이에서 테스트해본 결과입니다. REAPER -> OBS -> REAPER로 라우팅해서 테스트해보니 무려


![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2021-06-02-vst-plugin-delay/01b6aa9c78abe3d2d207094d8f00a581.png){: .align-center}  

9600 samples......... 0.2초......

이야.......

심지어 켤 때마다 조금씩 바뀌는게 컴 자원 사용량에 무언가 관련되어있지는 않을까 의심이 됩니다. 



그래서 얘를 사용해서 DAW를 활용하시려면 

1. OBS에서 윈도우즈 소리를 잡아서 ReaStream으로 DAW로 넘기고 OBS에서는 Mute하고

2. DAW에서 ASIO 입력으로 본인 목소리를 받고 

3. 빈 트랙에다 ReaStream으로 윈도우즈 소리를 잡고

4. 둘 다 라이브 모니터링을 켠 다음에 

5. 이 두 트랙을 잘 프로세싱한 다음 Mix bus로 묶어서 ReaStream으로 OBS에 보내신다면 

마이크와 윈도우즈 소리(주로 MR) 사이에 레이턴시 없이 송출 가능합니다. 방송 화면하고의 차이는 생길 테니 화면에 딜레이를 빡시게 주셔야겠죠. 



Q) 왜 이렇게까지 하나요? 

A) OBS는 공식적으로 Asio를 지원하지 않아서 기껏 좋은 오인페를 사도 안정적이고 빠른 Asio 드라이버를 버리고 딜레이 오지는 WDM 드라이버로밖에 활용을 못 해서 그럽니다. 그러면 OBS에서는 뭔 짓을 해도 본인 마이크 소리에 레이턴시가 끼고, 비싼 돈 날렸다고 착각하실 수 있습니다. 

대안으로 OBS-ASIO 라는 확장 플러그인이 있어서 OBS에서 ASIO 입력을 받을 수는 있습니다. 근데 공식 지원이 아니라서 그런지 DAW랑 같이 쓰다 보면 좀 불안정해서 OBS만 켜서 그 안에서 끝장을 봐야 합니다. 이것 관련해서 포스팅할 수도 있겠네요. 혹은 ReaRoute로 REAPER를 활용하거나 ASIO LINK PRO, VoiceMeeter같이 라우팅 프로그램을 쓰거나 해야 합니다.



여튼, 노래 방송 하는데 뭔가 레이턴시 때문에 이상하다 싶으시면 한 번쯤 플러그인이 자체 딜레이가 있는지 확인해보시는 것도 좋을 것 같습니다. 

피드백 환영합니다!
