---
title:   "DAW를 사용해서 OBS로 마이크 세팅하기"
excerpt: "세팅"
date:  2024-10-27 00:19:05 +0900

categories:
  - Setup

tags:
  - DAW
  - OBS
--- 

## 시작하기  

이 포스트는 DAW를 사용하여 마이크를 세팅하고, OBS로 소리를 빼는 방법을 소개하는 포스트입니다.  
오디오 인터페이스를 사용하는 것을 가정하고 있습니다.  
DAW는 REAPER v7.26, OBS 버전 30.2.3, obs-asio v3.2.1f을 사용하였습니다.  

### 마이크 주의사항  

마이크에 로우컷이나 -10dB Pad가 들어가있을 수 있습니다.  
이는 드럼이나 기타 앰프, 관악기 등 고음압, 저역대가 과한 음원에 주로 사용하는 것으로 보컬에서는 잘 쓰지 않습니다.  
혹은 하드웨어 컴프레서를 거쳐야 하는데 EQ가 없다, 할 때 씁니다.  

제조사마다 다른데, 500Hz까지 영향을 받기 때문에 보컬 마이크에서 사용하기에는 명확한 의도가 있을 때만 사용합니다.  
잘 확인해서 잘 꺼둡시다.  

참고하면 좋을 글  
[https://kiriki-liszt.github.io/yg331/daw/recording-clipping/](https://kiriki-liszt.github.io/yg331/daw/recording-clipping/)  

### 오인페의 다이렉트 모니터링  

이 글은 DAW에서 EQ, 컴프레서, 리버브 등을 듣는 것을 전제로 하기 때문에 오인페의 내장 기능인 다이렉트 모니터링은 꺼두셔야 합니다.  
만약 켜져있다면 목소리가 두 번 들리게 되니 주의하시기 바랍니다.  

## DAW 세팅하기  

### REAPER 설치, 스킨 적용  

가장 최신의 REAPER를 설치해줍니다.  
설치 시, 세부 옵션에서 ReaRoute가 선택되어 있는지 확인합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_install_options.png){: .align-center}  

기본 스킨은 아쉬우니 기본에서 벗어나지 않고 가독성을 늘려주는 스킨인 ReaperTips를 설치합니다.  

[https://www.reapertips.com/resources/reapertips-theme](https://www.reapertips.com/resources/reapertips-theme)  

I Want This! -> 가격 $0.00 입력 -> 이메일 입력 -> Download now! -> 받은 메일에서 링크를 통해 다운로드  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_theme_install_.png){: .align-center}  

파일의 압축을 풀고 각자의 운영체제에 맞는 폴더로 가서 Reapertips Theme.ReaperThemeZip를 더블클릭해 스킨을 적용합니다.  

### 플러그인 설치  

#### EQ, Compressor, Saturation  

메인 마이크 트랙에 주로 사용할 플러그인은 제가 오픈 소스로 소스코드를 공개해서 개발한 플러그인들을 사용하겠습니다.  

[https://github.com/Kiriki-liszt/Relief_EQ](https://github.com/Kiriki-liszt/Relief_EQ)  

[https://github.com/Kiriki-liszt/Relief_Compressor](https://github.com/Kiriki-liszt/Relief_Compressor)  

[https://github.com/Kiriki-liszt/JS_Inflator](https://github.com/Kiriki-liszt/JS_Inflator)  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/VST_plugins_homepage_.png){: .align-center}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/VST_plugins_download.png){: .align-center}  

각 페이지에서 설명을 읽어볼 수 있고, 우측의 Release 페이지에서 최신 릴리즈를 선택, 운영체제에 맞게 다운로드합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/VST_plugins_install.png){: .align-center}  

파일의 압축을 풀고, .vst3 파일을 C:\Program Files\Common Files\VST3 폴더로 옮겨줍니다.  
정리하는 취향에 따라 VST3 폴더 아래애 새로운 폴더를 만들고, 그 안에 정리해도 됩니다.  

#### EFX  

전화통화 느낌의 특수효과로는 Lese의 Codec을 사용하겠습니다.  
이는 실제 음성통화에 사용하는 낮은 음성싱호 대역폭과 비트레이트 제한을 그대로 재현하거나, 핸드폰 컬러링이나 인터넷 초창기의 저음질 mp3 느낌을 낼 수 있습니다.  

[https://lese.io/plugin/codec/](https://lese.io/plugin/codec/)  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/Lese-codec-homepage.png){: .align-center}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/Lese-codec-email-sent.png){: .align-center}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/Lese-codec-email-installer.png){: .align-center}  

이메일을 입력하면 설치 파일에 대한 링크가 포함된 이메일을 받습니다.  
운영체제에 해당하는 파일을 다운로드받아 설치합니다.  

#### Reverb  

리버브는 취향을 많이 타기 때문에, 본인이 원하는 사운드가 있다면 그 소리를 내는 리버브를 사용하시면 됩니다.  

하지만 그냥 제일 무난하고 어디에도 잘 붙는 스타일을 원하신다면, 대부분 부드러운 톤의 Hall 타입입니다.  
이 글에서는 그 예시로 Voxengo의 OldSkoolVerb를 사용합니다.  
제일 정석적이고 부드러운 성향입니다.  

[https://www.voxengo.com/product/oldskoolverb](https://www.voxengo.com/product/oldskoolverb)  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/Voxengo_download.png){: .align-center}  

우측에서 운영체제에 맞게 다운로드, 설치해줍니다.  

이외에 제일 많이 추천되는 리버브는 Denis Tihanov의 OrilRiver입니다.  

[https://www.kvraudio.com/product/orilriver-by-denis-tihanov](https://www.kvraudio.com/product/orilriver-by-denis-tihanov)

우측의 윈도우와 맥 아이콘이 있고 그 오른쪽에 최신 버전의 설치 파일을 다운로드 받을 수 있습니다.  

취향에 따라 Native Instruments의 Raum도 좋습니다.  
좀 더 실험적이고 짙은 질감의 성향입니다.  

[https://www.native-instruments.com/en/products/komplete/effects/raum/](https://www.native-instruments.com/en/products/komplete/effects/raum/)

우측의 Free download with Komplete Start -> 로그인 or 회원가입 -> get Komplete Start -> 운영체제에 맞게 다운로드 -> 설치 -> Native Access 실행 -> Raum 설치  
이때, 윈도우 사용자 이름이 한글일 경우 에러가 발생하니, 포맷이 쉽지 않다면 빠른 포기.  

프리셋을 사용하지 않고 세팅을 하나하나 설정하기 원한다면 Airwindows의 리버브들이나 Mverb2020 등도 좋은 소리를 가지고 있습니다.  

### REAPER 환경설정  

처음 REAPER를 실행했다면, 오디오 디바이스를 설정해야 합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_option_screen_1.png){: .align-center}  

상단바의 Options -> preferences로 들어가 환경 설정창을 엽니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_option_screen_2_.png){: .align-center}  

우선은 Audio 페이지를 찾아 엽니다.  
맨 위에 있는 체크박스, Close audio device when ~~~ 옵션을 꺼줍니다.  
우하단의 Apply를 눌러 설정을 저장하고 다음 페이지로 넘어갑니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_option_screen_3_.png){: .align-center}  

이어서 Audio -> device에서 Audio를 ASIO로 설정합니다.  
바로 밑에서 Asio Driver를 사용하는 오디오 인터페이스를 선택합니다.  
이어서 입출력이 올바르게 잡힌 것을 확인합니다.  
확실하지 않다면, 입력 1/2번을 오인페의 입력 1/2로, 출력 1/2번을 오인페의 출력 1/2로 잡아줍니다.  

아래의 두 체크박스를 모두 켜 줍니다.  
Request sample rate는 48000, Request block size는 64 / 128 / 256 /512 중에서 컴퓨터가 버티는 한 제일 작게 해 줍니다.  
Block size가 작을 수록 본인이 모니터링 할 때 들리는 레이턴시가 줄어듭니다.  
다만 64 이하의 버퍼 사이즈는 CPU에 부담을 많이 주어 찢어지거나 후두둑 뜯기는 소리를 유발할 가능성이 높습니다.  
만약 본인의 PC 사양이 높아 견딜 수 있다면, 물론 64 버퍼 사이즈로 가는 것이 좋습니다.  
아니더라도 128 버퍼 사이즈도 거의 레이턴시를 느끼지 못 할 수준입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_option_screen_4.png){: .align-center}  

아래의 ASIO Configuration을 눌러 오인페 설정창을 열어 동일하게 설정해줍니다.  

혹시 해서 확인하자면, 모든 오디오의 Sample rate는 자동으로 맞춰지겠지만, 가능한 한 모두 같은 48000으로 통일하시기 바랍니다.  
윈도우 출력장치, 녹음 장치, OBS의 오디오 샘플레이트(48kHz), 오인페의 설정, DAW의 샘플레이트를 모두 같은 48000으로 설정합니다.  

우하단의 Apply를 눌러 설정을 저장합니다.  
설정 창을 닫습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_option_screen_5.png){: .align-center}  

REAPER의 메인 화면으로 돌아와, 우측 상단에는 현재 사용중인 오디오 디바이스와 샘플링 레이트, 입출력 레이턴시가 ms 단위로 표시됩니다.  
윈도우 기준, sampling rate 48000Hz, buffer size 128에서 포커스라이트의 Clarett 2Pre의 입출력 레이턴시는 6.2/8.2 ms가 나왔습니다.  
보통의 경우, 10~12ms의 레이턴시는 뇌에서 딜레이라고 느끼지 못하는 수준입니다.  
심지어 그랜드 피아노의 건반을 누르고 연주자에게 소리가 들리기까지의 레이턴시는 30ms정도 걸리지만, 아무 문제 없습니다.  
드럼이 들어갈 만한 크기의 합주실에서 연습할 때 보컬과 드럼이 5m 떨어져 있고 보컬 스피커가 드럼 뒤에 있다면 대략 15ms의 딜레이가 있지만, 마찬가지로 아무 문제 없습니다.  
그러므로 128 버퍼 사이즈의 총 레이턴시 14.4ms는 실시간 모니터링에 사용할 만한 수준입니다.  
하지만 256 버퍼 사이즈부터는 11/13 = 24ms의 레이턴시로 딜레이가 체감되어 문제가 되기 시작하고, 512 버퍼 사이즈는 22/24 = 46ms의 레이턴시로 실시간 모니터링이 불가해집니다.  

참고로 맥의 Core Audio에서는  
64 - 4.5/4.3 ms  
128 - 5.9/5.6 ms  
256 - 8.5/8.3 ms  
512 - 13/13 ms  
의 레이턴시를 가집니다.  

### REAPER 마이크 트랙 세팅  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_main_screen_1_.png){: .align-center}  

메인 화면의 하단 믹서 창에서 빈 공간을 더블클릭해 새 트랙을 하나 생성합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_main_screen_2_.png){: .align-center}  

맨 아래쪽에 트랙 숫자 바로 위를 클릭해 트랙 이름을 지정할 수 있습니다.  
본인이 알아볼 수 있도록 Vocal, Mic 등으로 이름을 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_main_screen_3_.png){: .align-center}  

트랙 슬라이더의 오른쪽에 여러 버튼들이 있을텐데, (M)ute 와 (S)olo 버튼, 그 위에 아래를 향하는 스피커 버튼, 그리고 그 위에 흰 동그라미(도넛모양) 버튼을 찾습니다.  
동그라미 버튼이 라이브 모니터링 버튼으로, 클릭해서 활성화시킨다면 이제 본인 목소리를 DAW를 통해 들을 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_main_screen_4_.png){: .align-center}  

REAPER에서 자동으로 새 트랙을 생성할 때, 오인페의 왼쪽(1번) 입력만을 모노로 받는 트랙으로 생성합니다.  
만약 소리가 한 쪽만 난다거나, 안 난다거나 하면 이 설정이 꼬인 것입니다.  
트랙의 슬라이더 위에 IN 버튼 위에 오인페 입력이 적혀있는 곳을 클릭합니다.  
Input Mono로 들어가 사용하고자 하는 오인페 입력을 선택해주어 설정합니다.  

플러그인을 불러오기 전에, 오인페의 적정 게인=레벨=마이크볼륨을 설정해야 합니다.  
실제 노래방송을 하듯이 유튜브에서 Inst를 틀고, 본인 목소리 크기는 신경쓰지 말고 일단 불렀을 때 오인페에서 주황불이 겨우 들어올락 말락 할 때 까지 "오인페"의 게인을 조절합니다.  
DAW나 윈도우 녹음장치가 아닌 하드웨어 오인페의 게인을 조정합니다.  
그리고 다시 조금 줄입니다.  
이는 실제 방송이나 목인 풀린 상황에서는 더 큰 볼륨이 나오기 때문에, 오인페단에서부터 소리가 깨져버린다면 플러그인으로 더 악화되기 때문입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_FX_1_.png){: .align-center}  

해당 트랙의 중간에 있는 FX 버튼을 눌러 플러그인 창을 켭니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_FX_2_.png){: .align-center}  

제일 먼저 ReaGate를 추가해 배경으로 깔리는 잡음을 줄입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_gate_threshold_set.png){: .align-center}  

좌측의 미터를 보고 조용히 있을 때의 입력 레벨을 확인, 이것보다 조금 높게 Threshold를 설정합니다.  
공기청정기가 중간 세기로 돌아가고 있는 방에서 오인페와 컨덴서 마이크를 사용하고, 오인페 게인을 3/4 정도로 두었을 때 노이즈 플로어는 -60dB 정도 나왔습니다.  

이를 기준으로 본다면, 여유롭고 넉넉하게 -50dB의 Threshold를 두면 충분합니다.  
노이즈 플로어와 목소리 크기의 차이는 SNR 이라 하며 30 ~ 45dB 이상의 차이를 가지는게 좋습니다.  
만약 Inst를 들으며 노래를 할 때의 볼륨이 노이즈 플로어로부터 30dB의 차이도 나지 않는다면, 마이크/오인페가 고장났거나, 마이크 방향을 반대로 쓰고 있거나, 마이크로부터 너무 멀리 떨어져 있는 상태입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_gate_setting.png){: .align-center}  

PreOpen 1ms, Attack 1ms, Release 100ms, Hysteresis -3dB로 세팅합니다.  
PreOpen은 레이턴시와 직결되므로, 1ms보다 넘지 않도록 꼭 주의해서 값을 직접 입력합니다.  
마지막으로 오른쪽의 Dry 슬라이더를 -18dB정도로 올려서, Gate ON / Off의 전환이 덜 급격하게 합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_EQ_setting.png){: .align-center}  

다음으로 Relief EQ를 추가합니다.  
베이직한 보컬 EQ 세팅은 HighPass 60Hz 18dB/oct, Bell 220Hz 2.1Q -2.5dB, Bell 470Hz 1.7Q -1.5dB, Bell 4000Hz 2.1Q -2dB, High Shelf 16000Hz 4.5dB.  
여기에서 취향에 따라 저음을 덜 줄이거나, 고음을 덜 키우거나 할 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Comp_1_setting.png){: .align-center}  

Relief Compressor를 추가해 첫 번째 보컬 컴프레서로 사용합니다.  
최대한 가볍게 Attack 10ms, Release 120ms, Ratio 2, Knee 20dB으로 설정하고, Threshold를 조정해 조곤조곤 말할 때는 Gain Reduction이 반응하지 않게, 신나서 이야기할 때 -3 ~ -5dB 정도 걸리게 합니다.  
오인페 입력 조정이 잘 이루어졌다면, 보통 -20dB +-3dB 정도의 Threshold값이 나오게 됩니다.  
조정 결과 더 큰 Threshold(ex -6dB)가 나온다면 오인페 입력이 매우 크니, 줄여주시기 바랍니다.  
더 작다면 플러그인의 Input을 올려서 적정 범위 안에 들어오게 합니다.  
Makeup Gain은 2dB 정도 올려줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Comp_2_setting.png){: .align-center}  

Relief Compressor를 추가해 두 번째 보컬 컴프레서로 사용합니다.  
이는 조금 더 빡빡하게 Attack 6ms, Release 100ms, Ratio 4, Knee 5dB으로 설정하고, Threshold를 조정해 평소 말할 때와 적당히 노래할 때는 Gain Reduction이 반응하지 않게, 노래의 하이라이트를 부를 때 만 -3 ~ -5dB 정도 걸리게 합니다.  
Makeup Gain은 4dB 정도 올려줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Deesser_sidechain_eq.png){: .align-center}  

이어서 Relief Compressor를 하나 더 추가해서, Deesser로 사용합니다.  
플러그인 창에서 SIDECHAIN-EQ 탭을 열어 LF Freq 5500Hz, High - OFF로 설정합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Deesser_setting.png){: .align-center}  

다시 COMPRESSOR탭으로 돌아와 Attack 3ms, Release 20ms, Ration 20, Knee 0dB로 세팅 후 Threshold를 조정해 ㅅ, ㅆ, ㅊ, ㅉ 등의 치찰음들을 -3~6dB 정도 Gain Reduction이 일어나도록 합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Inflator_setting.png){: .align-center}  

마지막으로 JS Inflator를 추가합니다.  
Mix 노브를 100%까지 올리고, Output을 -3dB 정도 내립니다.  
-1dB로 하지 않는 이유는 후에 리버브가 추가되었을 때 볼륨이 올라가므로 약간의 여유를 둔 것입니다.  
더 힘있고 꽉 찬 소리를 원하면 Input을 키우고, 이미 과하다 싶으면 줄입니다.  
주의할 점은 Inst에 대고 노래를 부른다면 생각보다 힘이 밀릴 수 있으니 모니터링하면서 조절하지 말고, OBS 등으로 Inst와 함께 녹음된 것을 들어보고 판답합니다.  

여기까지의 총 레이턴시는 113 samples로, REAPER에서는 이를 Buffer Size의 정수 배로 처리해서 128 버퍼 사이즈의 레이턴시가 됩니다.  
sample rate 48000Hz에서 128 samples는 2.6ms로 총 입출력 레이턴시에 더해집니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_FX_PDC.png){: .align-center}  

이를 조금이라도 줄이는 방법은 FX 창의 빈 공간을 우클릭해 Chain DPC Mode -> ignore plugin delay로 설정한다면 Buffer Size의 정수 배가 아닌 총합 그대로 처리되어 0.3ms 정도를 줄일 수 있습니다.  
만약 이로도 부족하다면, ReaGate의 PreOpen를 0ms로 줄이고 Attack을 3~5ms까지 키워 말의 맨 앞 음절을 약간 손해를 보는 대신 1ms의 레이턴시를 더 줄일 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_1.png){: .align-center}  

이제 메인 보컬 트랙이 완성되었으니, 리버브 트랙을 추가합니다.  
마찬가지로 빈 공간을 더블클릭해 새 트랙을 추가합니다.  
이름은 Reverb 등으로 알아볼 수 있게 지어줍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_2_.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_3.png){: .align-center}  

다시 원래 보컬 트랙에서, (M)ute 아래에 (S)olo 버튼 아래에 세 줄이 그어진 버튼을 클릭합니다.  
이는 라우팅 설정 창으로, 여기에서 새로 만든 Reverb 트랙으로 소리를 보내주도록 합니다.  
좌측의 add new Send -> 방금 만든 Reverb트랙을 선택해 Send를 만들어줍니다.  
이제 메인 트랙의 소리가 Reverb 트랙으로도 들어가고 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_4.png){: .align-center}  

Reverb 트랙의 FX 창을 열어 OldSkoolVerb를 추가합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_5_.png){: .align-center}  

불러온 직후, 우상단의 DRY MUTE를 켜서 오직 리버브 소리만 들리게 합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_6_.png){: .align-center}  

이제 좌상단의 Preset에 들어가 하나씩 들어보며 비교합니다.  
제일 무난하게 두루두루 어울리는 쪽은 warm hall, nice hall을 추천합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_8_.png){: .align-center}  

마지막으로 해당 트랙의 볼륨 슬라이더를 조정해 리버브의 비율을 조절합니다.  
노래를 부르는 본인에게는 리버브가 적어보일 수 있으나, 막상 OBS로 녹화해보면 생각보다 클 수 있으니 이 또한 꼭 녹화해서 들어보시기 바랍니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Reverb_9_.png){: .align-center}  

리버브를 끌 때는 해당 트랙을 뮤트합니다.  

### 보컬 트랙에 특수 효과(오래된 라디오/전화기 등등) 추가하기  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Codec_setting.png){: .align-center}  

상기한 Lese Codec 플러그인을 메인 마이크 트랙에 추가한다면 기본 세팅에서 그대로 훌륭한 Lofi 전화통와 음질을 얻을 수 있습니다.  
추가하는 위치는 Inflator 바로 이전을 추천하지만, 이 뒤에 추가하더라도 문제는 없습니다.  
다만, 이 플러그인은 65ms의 레이턴시를 가지므로 필요할 때만 켜주고, 이외의 경우 항상 완전히 꺼두는 것을 추천합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/FX_Codec_off_.png){: .align-center}  

믹서 창에서 플러그인들이 이름으로 쭈루룩 나열되어 있는 부분에서 쉬프트+클릭 단축키로 켜고 끌 수 있습니다.  

### REAPER 출력단 설정  

이제 하단 믹서창의 제일 왼쪽의 Master 트랙에서 출력되는 위치를 설정합니다.  
기본적으로 오디오 인터페이스의 출력단이 설정되어 있을 겁니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Master_out_1_.png){: .align-center}  

슬라이더 오른쪽의 세 줄 버튼을 눌러 라우팅 설정 창을 켭니다.  
Add new Hardware output -> ReaRoute 1 / 2 를 골라 1번 2번 두 트랙으로 나가는 출력을 추가합니다.  
이 ReaRoute 1/2가 왼쪽 오른쪽 트랙이 되어 OBS로 들어가게 됩니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/REAPER_Master_out_2__.png){: .align-center}  

여기서 OBS로 가는 소리의 크기 말고, 본인의 오인페 출력의 소리 크기를 설정할 수 있습니다.  
기존에 추가되어 있는 하드웨어 출력의 슬라이더를 움직여 크기를 조절할 수 있습니다.  

## OBS 셋업하기  

### OBS 준비  

우선 최신 버전으로 업데이트합니다.  
이어서 OBS에서 ASIO 장치를 사용할 수 있는 obs-asio를 설치합니다.  

[https://github.com/Andersama/obs-asio](https://github.com/Andersama/obs-asio)  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/obs-asio_homepage.png){: .align-center}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/obs-asio_download.png){: .align-center}  

우측의 Release에서 가장 최신의 Release를 선택해 설치 파일을 다운로드합니다.  
설치가 완료되면 OBS를 실행합니다.  

### OBS 환경설정  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/OBS_setting_output.png){: .align-center}  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/OBS_setting_audio.png){: .align-center}  

OBS의 설정 -> 출력 탭에서 오디오 비트레이트 320kbps로 올려줍니다.  
오디오 탭에서 샘플 레이트 48kHz로 설정합니다.  
마이크/aux 오디오는 전부 비활성화합니다.  

### OBS 소스 설정

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/ASIO_input_capture_1.png){: .align-center}  

기본 화면에서 소스 추가 -> ASIO Input Capture를 추가합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/ASIO_input_capture_2.png){: .align-center}  

Device는 ReaRoute ASIO로 설정합니다.  
OBS 채널 1 / 2에 각각 ReaRoute 1/2를 할당합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/ASIO_input_capture_3.png){: .align-center}  

아래의 control page를 켜서 sample format을 32bit float으로 설정합니다.  
OBS를 재시작합니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-10-27/ASIO_input_capture_4.png){: .align-center}  

재시작 이후, REAPER의 소리가 OBS에서 잘 잡히는 것을 확인할 수 있습니다.  

모든 것이 잘 자리잡았다면 사용하지 않는 마이크 오디오 소스와 마이크/aux를 정리해야 합니다.  
거기에 설정해놓은 플러그인 등이 사용되고 있지 않을 때에도 항상 cpu 자원을 사용하고 있기 때문에, 없에버려야 합니다.  
걱정이시라면 모두 스크린샷을 해서 보관해두시는 것도 좋습니다.  

## 볼륨 밸런스 맞추기  

유튜브, 게임 등의 볼륨은 풀볼륨으로 리셋되는 경우가 있으니, 풀볼륨으로 맞추고 오인페의 하드웨어 볼륨을 줄여서 맞춥니다.  
이때 윈도우 볼륨도 꼭 100으로 고정해둡니다.  
그 다음에 REAPER의 Master단 Send 라우팅에서 볼륨을 조절해 본인 목소리 모니터링 볼륨을 조절합니다.  
그리고 마지막으로 OBS에서 데스크탑 볼륨과 마이크 볼륨의 비율을 맞춥니다.  

OBS에서 마이크 볼륨이 빨간색에만 안 들어가게 하시면 됩니다.  

## 주의사항  

켤 때는 REAPER를 먼저 켜고 OBS를 나중에 켜야 합니다.  
반대로 끌 때는 OBS를 먼저 끈 다음 REAPER를 꺼야 합니다.  
만약 REAPER가 먼저 꺼진다면, 글리치 노이즈가 OBS로 들어가게 되니 바로 트랙을 꺼 주시기 바랍니다.  
