---
title:   "VSTSDK 사용 시 Mac에서 AUv2로 빌드하기"
excerpt: "플러그인을 만들어보자!"
date:  2023-10-21 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 시작하기  

VSTSDK 3.7.9, intel iMac 21.5(Retina 4K, 2019년), Xcode 15.0.1를 사용했다.  
여담이지만 Xcode 15 정말 느려터졌다.  

## CoreAudio setup  

AUv2 Wrapper를 사용하기 위해선 CoreAudio 클래스가 정의되어 있는 폴더가 필요하다.  
<https://developer.apple.com/library/archive/samplecode/CoreAudioUtilityClasses/Introduction/Intro.html>  
해당 페이지의 Download Sample Code를 클릭해 다운로드할 수 있다.  
압축을 풀고 CoreAudio 폴더를 vst3sdk와 같은 레벨로 이동한다.  

## VSTSDK setup  

처음은 vst3sdk/cmake/modules/SMTG_AddVST3AuV2.cmake의 line.8~18 코드의 set문 두개를 밑에 있는 function(smtg_target_add_auv2 target) 안으로 복사해 붙여넣는다.  

다음은 vst3sdk/CMakeLists.txt 에서 line.10~11 에서 두 옵션을 OFF로 꺼준다.  
line.71에 있는 add_subdirectory 아래에 include(SMTG_AddVST3AuV2) 한 줄을 추가한다.  

마지막으로 VST3_Project_Generator/macOS/VST3_Project_Generator.app/Contents/Resources/cmake/templates/vst3plugin_folder/CMakeLists.txt.in 파일의 텍스트를 수정할 것이다.  
맨 끝에 다음의 코드를 추가한다.  

``` cmake
# Add an AUv2 target
if (SMTG_MAC AND XCODE AND SMTG_COREAUDIO_SDK_PATH)
    smtg_target_add_auv2(@SMTG_CMAKE_PROJECT_NAME@-au
        BUNDLE_NAME @SMTG_CMAKE_PROJECT_NAME@
        BUNDLE_IDENTIFIER @SMTG_PLUGIN_IDENTIFIER@.audiounit
        INFO_PLIST_TEMPLATE resource/au-info.plist
        VST3_PLUGIN_TARGET @SMTG_CMAKE_PROJECT_NAME@)
endif(SMTG_MAC AND XCODE AND SMTG_COREAUDIO_SDK_PATH)
```

## Generator 사용하여 프로젝트 생성  

이제 VST3_Project_Generator 에서 맞는 운영체제에 해당하는 실행파일로 프로젝트를 생성하면 AUv2 Wrapper를 추가해 빌드할 수 있다.  
이 부분은 추가할 내용이 없다.  

## CMakeList 수정  

생성된 프로젝트의 최상위 폴더에 CMakeList가 하나 만들어져 있을 것이다.  

중간에 #- VSTGUI Wanted ---- 영역의 smtg_target_add_plugin_resources 함수의 인자 리스트에 GUI에 필요한 리소스들을 다 추가해준다.  

## info.plist 수정  

vst3sdk/public.sdk/samples/vst/again/resource/au-info.plist를 복사해 생성된 프로젝트의 resource 폴더로 붙여넣는다.  
복사한 plist에서 다음과 같이 array로 감싸진 부분을 수정한다.  
이때 이름이 아무리 달라도 동일한 제조사, 동일한 type라면 subtype으로 플러그인을 구분하므로 같은 subtype을 사용하지 않도록 하자.  
예시는 다음과 같다.  

``` plist
 <array>
  <dict>
   <key>factoryFunction</key>
   <string>AUWrapperFactory</string>
   <key>description</key>
   <string>AGain</string>
   <key>manufacturer</key>
   <string>Stgb</string>
   <key>name</key>
   <string>Steinberg: AGain</string>
   <key>subtype</key>
   <string>gain</string>
   <key>type</key>
   <string>aufx</string>
   <key>version</key>
   <integer>0xFFFFFFFF</integer>
  </dict>
 </array>
```

``` plist
<array>
  <dict>
   <key>description</key>
   <string></string>
   <key>factoryFunction</key>
   <string>OxfordInflatorAUFactory</string>
   <key>manufacturer</key>
   <string>Sony</string>
   <key>name</key>
   <string>Sonnox: Oxford Inflator</string>
   <key>subtype</key>
   <string>OxIn</string>
   <key>type</key>
   <string>aufx</string>
   <key>version</key>
   <integer>262144</integer>
  </dict>
 </array>
```

## 그러면 끝  

이제 문제 없이 컴파일과 빌드가 마무리되어야 할 것이다.  
디버깅 모드로 빌드하여 VSTGUI WYSIWYG 에디터를 사용한다면 아마 처음에는 검은 화면만 나타날 것이다.  
좌상단의 edit을 잘 클릭해서 열고, 리소스와 배경 등을 잘 추가하고 파라미터를 연결하고 저장하면 새로운 GUI로 잘 나타날 것이다.  
