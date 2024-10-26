---
title:   "DAW를 사용해서 OBS로 마이크 세팅하기"
excerpt: "세팅"
date:  2024-10-26 00:19:05 +0900

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

## DAW 세팅하기  

### REAPER 설치, 스킨 적용  

가장 최신의 REAPER를 설치해줍니다.  
설치 시, 세부 옵션에서 ReaRoute가 선택되어 있는지 확인합니다.  

기본 스킨은 아쉬우니 기본에서 벗어나지 않고 가독성을 늘려주는 스킨인 ReaperTips를 설치합니다.  

[https://www.reapertips.com/resources/reapertips-theme](https://www.reapertips.com/resources/reapertips-theme)  

I Want This! -> 가격 $0.00 입력 -> 이메일 입력 -> Download now! -> 받은 메일에서 링크를 통해 다운로드  

파일의 압축을 풀고 각자의 운영체제에 맞는 폴더로 가서 Reapertips Theme.ReaperThemeZip를 더블클릭해 스킨을 적용합니다.  

### 플러그인 설치  

메인 마이크 트랙에 사용할 플러그인은 제가 오픈 소스로 소스코드를 공개해서 개발한 플러그인들을 사용하겠습니다.  
각 페이지에서 설명을 읽어볼 수 있고, 우측의 Release 페이지에서 최신 릴리즈를 선택, 운영체제에 맞게 다운로드합니다.  
파일의 압축을 풀고, .vst3 파일을 C:\Program Files\Common Files\VST3 폴더로 옮겨줍니다.  

[https://github.com/Kiriki-liszt/Relief_EQ](https://github.com/Kiriki-liszt/Relief_EQ)  

[https://github.com/Kiriki-liszt/Relief_Compressor](https://github.com/Kiriki-liszt/Relief_Compressor)  

[https://github.com/Kiriki-liszt/JS_Inflator](https://github.com/Kiriki-liszt/JS_Inflator)  

리버브 플러그인은 Voxengo의 OldSkoolVerb를 사용합니다.  
제일 정석적이고 부드러운 성향입니다.  

[https://www.voxengo.com/product/oldskoolverb](https://www.voxengo.com/product/oldskoolverb)  

우측에서 운영체제에 맞게 다운로드, 설치해줍니다.  

취향에 따라 Native Instruments의 Raum도 좋습니다.  
좀 더 실험적이고 짙은 질감의 성향입니다.  

[https://www.native-instruments.com/en/products/komplete/effects/raum/](https://www.native-instruments.com/en/products/komplete/effects/raum/)

우측의 Free download with Komplete Start -> 로그인 or 회원가입 -> get Komplete Start -> 운영체제에 맞게 다운로드 -> 설치 -> Native Access 실행 -> Raum 설치  
이때, 윈도우 사용자 이름이 한글일 경우 에러가 발생하니, 포맷이 쉽지 않다면 빠른 포기.  

### REAPER 환경설정  

처음 REAPER를 실행했다면, 오디오 디바이스를 설정해야 합니다.  
상단바의 Options -> preferences로 들어가 환경 설정창을 엽니다.  

우선은 Audio 페이지를 찾아 엽니다.  
맨 위에 있는 체크박스, Close audio device when ~~~ 옵션을 꺼줍니다.  
우하단의 Apply를 눌러 설정을 저장하고 다음 페이지로 넘어갑니다.  

이어서 Audio -> device에서 Audio를 ASIO로 설정합니다.  
바로 밑에서 Asio Driver를 사용하는 오디오 인터페이스를 선택합니다.  
이어서 입출력이 올바르게 잡힌 것을 확인합니다.  
확실하지 않다면, 입력 1/2번을 오인페의 입력 1/2로, 출력 1/2번을 오인페의 출력 1/2로 잡아줍니다.  

아래의 두 체크박스를 모두 켜 줍니다.  
Request sample rate는 48000, Request block size는 16 / 32 / 64 / 128 / 256 중에서 컴퓨터가 버티는 한 제일 작게 해 줍니다.  
Block size가 작을 수록 본인이 모니터링 할 때 들리는 레이턴시가 줄어듭니다.  
아래의 ASIO Configuration을 눌러 오인페 설정창을 열어 동일하게 설정해줍니다.  

혹시 해서 확인하자면, 모든 오디오의 Sample rate는 자동으로 맞춰지겠지만, 가능한 한 모두 같은 48000으로 통일하시기 바랍니다.  
윈도우 출력장치, 녹음 장치, OBS의 오디오 샘플레이트(48kHz), 오인페의 설정, DAW의 샘플레이트를 모두 같은 48000으로 설정합니다.  

우하단의 Apply를 눌러 설정을 저장합니다.  
설정 창을 닫습니다.  

### REAPER 마이크 트랙 세팅  

메인 화면의 하단 믹서 창에서 빈 공간을 더블클릭해 새 트랙을 하나 생성합니다.  
맨 아래쪽에 트랙 숫자 바로 위를 클릭해 트랙 이름을 지정할 수 있습니다.  
본인이 알아볼 수 있도록 Vocal, Mic 등으로 이름을 지어줍니다.  
트랙 슬라이더의 오른쪽에 여러 버튼들이 있을텐데, (M)ute 와 (S)olo 버튼, 그 위에 아래를 향하는 스피커 버튼, 그리고 그 위에 흰 동그라미(도넛모양) 버튼을 찾습니다.  
동그라미 버튼이 라이브 모니터링 버튼으로, 클릭해서 활성화시킨다면 이제 본인 목소리를 DAW를 통해 들을 수 있습니다.  

REAPER에서 자동으로 새 트랙을 생성할 때, 오인페의 왼쪽(1번) 입력만을 모노로 받는 트랙으로 생성합니다.  
만약 소리가 한 쪽만 난다거나, 안 난다거나 하면 이 설정이 꼬인 것입니다.  
트랙의 슬라이더 위에 IN 버튼 위에 오인페 입력이 적혀있는 곳을 클릭합니다.  
Input Mono로 들어가 사용하고자 하는 오인페 입력을 선택해주어 설정합니다.  

플러그인을 불러오기 전에, 오인페의 적정 게인=레벨=마이크볼륨을 설정해야 합니다.  
실제 노래방송을 하듯이 유튜브에서 Inst를 틀고, 본인 목소리 크기는 신경쓰지 말고 일단 불렀을 때 오인페에서 주황불이 겨우 들어올락 말락 할 때 까지 게인을 조절합니다.  
그리고 다시 조금 줄입니다.  
이는 실제 방송이나 목인 풀린 상황에서는 더 큰 볼륨이 나오기 때문에, 오인페단에서부터 소리가 깨져버린다면 플러그인으로 더 악화되기 때문입니다.  

해당 트랙의 중간에 있는 FX 버튼을 눌러 플러그인 창을 켭니다.  
제일 먼저 Relief EQ를 추가합니다.  
베이직한 보컬 EQ 세팅은 HighPass 60Hz 18dB/oct, Bell 220Hz 2.14Q -2.5dB, Bell 470Hz 1.78Q -1.5dB, Bell 4000Hz 2.1Q -2dB, High Shelf 16000Hz 5dB.  

다음으로 Relief Compressor를 추가해 메인 보컬 컴프레서로 사용합니다.  
이 또한 안전한 세팅으로 Attack 6ms, Release 100ms, Ratio 4, Knee 20dB으로 설정하고, Threshold를 조정해 조곤조곤 말할 때는 Gain Reduction이 반응하지 않게, 신나서 말할 때 -3~4dB, 크게 노래부를 때 -5~7dB 정도 걸리게 합니다.  
오인페 입력 조정이 잘 이루어졌다면, 보통 -18dB +-3dB 정도의 Threshold값이 나오게 됩니다.  
조정 결과 더 큰 Threshold(ex -6dB)가 나온다면 오인페 입력이 매우 크니, 줄여주시기 바랍니다.  
더 작다면 플러그인의 Input을 올려서 적정 범위 안에 들어오게 합니다.  
Makeup Gain은 5dB 정도 올려줍니다.  

이어서 Relief Compressor를 하나 더 추가해서, Deesser로 사용합니다.  
플러그인 창에서 SIDECHAIN-EQ 탭을 열어 LF Freq 5500Hz, High - OFF로 설정합니다.  
다시 COMPRESSOR탭으로 돌아와 Attack 3ms, Release 20ms, Ration 20, Knee 0dB로 세팅 후 Threshold를 조정해 ㅅ, ㅆ, ㅊ, ㅉ 등의 치찰음들을 -3~6dB 정도 Gain Reduction이 일어나도록 합니다.  

마지막으로 JS Inflator를 추가합니다.  
Mix 노브를 100%까지 올리고, Output을 -1dB 정도 내립니다.  
더 힘있고 꽉 찬 소리를 원하면 Input을 키우고, 이미 과하다 싶으면 줄입니다.  
주의할 점은 Inst에 대고 노래를 부른다면 생각보다 힘이 밀릴 수 있으니 모니터링하면서 조절하지 말고, OBS 등으로 Inst와 함께 녹음된 것을 들어보고 판답합니다.  

이제 메인 보컬 트랙이 완성되었으니, 리버브 트랙을 추가합니다.  
마찬가지로 빈 공간을 더블클릭해 새 트랙을 추가합니다.  
이름은 Reverb 등으로 알아볼 수 있게 지어줍니다.  
다시 원래 보컬 트랙에서, (M)ute 아래에 (S)olo 버튼 아래에 세 줄이 그어진 버튼을 클릭합니다.  
이는 라우팅 설정 창으로, 여기에서 새로 만든 Reverb 트랙으로 소리를 보내주도록 합니다.  
좌측의 add new Send -> 방금 만든 Reverb트랙을 선택해 Send를 만들어줍니다.  
이제 메인 트랙의 소리가 Reverb 트랙으로도 들어가고 있습니다.  

Reverb 트랙의 FX 창을 열어 OldSkoolVerb를 추가합니다.  
불러온 직후, 우상단의 DRY MUTE를 켜서 오직 리버브 소리만 들리게 합니다.  
이제 좌상단의 Preset에 들어가 하나씩 들어보며 비교합니다.  
제일 무난하게 두루두루 어울리는 쪽은 warm hall, nice hall을 추천합니다.  
마지막으로 해당 트랙의 볼륨 슬라이더를 조정해 리버브의 비율을 조절합니다.  
노래를 부르는 본인에게는 리버브가 적어보일 수 있으나, 막상 OBS로 녹화해보면 생각보다 클 수 있으니 이 또한 꼭 녹화해서 들어보시기 바랍니다.  

### 보컬 트랙에 특수 효과(오래된 라디오/전화기 등등) 추가하기  

흔히 말하는 전화기 효과는 다운샘플링 한 신호를 좁게 BandPass 하는 것으로, 다운샘플링 과정에서 특유의 저음질이 나타나고, band pass 과정에서 특징적인 성향이 나옵니다.  

### REAPER 출력단 설정  

이제 하단 믹서창의 제일 왼쪽의 Master 트랙에서 출력되는 위치를 설정합니다.  
기본적으로 오디오 인터페이스의 출력단이 설정되어 있을 겁니다.  
슬라이더 오른쪽의 세 줄 버튼을 눌러 라우팅 설정 창을 켭니다.  
Add new Hardware output -> ReaRoute 1 / 2 를 골라 1번 2번 두 트랙으로 나가는 출력을 추가합니다.  
이 ReaRoute 1/2가 왼쪽 오른쪽 트랙이 되어 OBS로 들어가게 됩니다.  

여기서 OBS로 가는 소리의 크기 말고, 본인의 오인페 출력의 소리 크기를 설정할 수 있습니다.  
기존에 추가되어 있는 하드웨어 출력의 슬라이더를 움직여 크기를 조절할 수 있습니다.  

## OBS 셋업하기  

### OBS 준비  

우선 최신 버전으로 업데이트합니다.  
이어서 OBS에서 ASIO 장치를 사용할 수 있는 obs-asio를 설치합니다.  

[https://github.com/Andersama/obs-asio](https://github.com/Andersama/obs-asio)  

우측의 Release에서 가장 최신의 Release를 선택해 설치 파일을 다운로드합니다.  
설치가 완료되면 OBS를 실행합니다.  

### OBS 환경설정  

OBS의 설정 -> 출력 탭에서 오디오 비트레이트 320kbps로 올려줍니다.  
오디오 탭에서 샘플 레이트 48kHz로 설정합니다.  
마이크/aux 오디오는 전부 비활성화합니다.  

### OBS 소스 설정

기본 화면에서 소스 추가 -> ASIO Input Capture를 추가합니다.  
Device는 ReaRoute ASIO로 설정합니다.  
OBS 채널 1 / 2에 각각 ReaRoute 1/2를 할당합니다.  
아래의 control page를 켜서 sample format을 32bit float으로 설정합니다.  
OBS를 재시작합니다.  

재시작 이후, REAPER의 소리가 OBS에서 잘 잡히는 것을 확인할 수 있습니다.  

모든 것이 잘 자리잡았다면 사용하지 않는 마이크 오디오 소스와 마이크/aux를 정리해야 합니다.  
거기에 설정해놓은 플러그인 등이 사용되고 있지 않을 때에도 항상 cpu 자원을 사용하고 있기 때문에, 없에버려야 합니다.  
걱정이시라면 모두 스크린샷을 해서 보관해두시는 것도 좋습니다.  
