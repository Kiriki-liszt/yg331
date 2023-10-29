---
title:   "VSTSDK 사용 시 윈도우 dll 단일 패키지로 빌드하기"
excerpt: "플러그인을 만들어보자!"
date:  2023-10-20 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 시작하기  

VSTSDK 3.7.9, 왼도우 10, VS2022 community를 사용했다.  

## VSTSDK setup  
  
우선은 vst3sdk\cmake\modules\SMTG_AddCommonOptions.cmake 파일의 line.16 코드에서 SMTG_CREATE_BUNDLE_FOR_WINDOWS 옵션을 OFF로 지정한다.  
그 밑에 있는 Symbolic link도 꺼두면 나쁘지 않다.  

다음은 vst3sdk\cmake\modules\SMTG_AddSMTGLibrary.cmake 에서 line.423 코드를 '#'을 붙여 주석처리 한다.  
윈도우에서 번들로 빌드할 때 사용하는 것 같은데, VSTSDK 3.7.7에서 이 라인이 추가되면서 단일 패키지로 빌드 시 빌드되지 않는 문제가 있다.  

마지막으로 vst3sdk\CMakeLists.txt 에서 line.10~11 에서 두 옵션을 OFF로 꺼주면 기본 설정이 완료된다.  

## Generator 사용하여 프로젝트 생성  

이제 VST3_Project_Generator 에서 맞는 운영체제에 해당하는 실행파일로 프로젝트를 생성하면 윈도우에서도 번들이 아닌 단일 패키지 파일, dll 파일로 플러그인을 빌드할 수 있다.  
이 부분은 추가할 내용이 없다.  

## CMakeList 수정  

생성된 프로젝트의 최상위 폴더에 CMakeList가 하나 만들어져 있을 것이다.  

중간에 #- VSTGUI Wanted ---- 영역의 smtg_target_add_plugin_resources 함수의 인자 리스트에 GUI에 필요한 리소스들을 다 추가해준다.  

그리고 resource\win32resource.rc 파일을 텍스트 에디터 등으로 직접 수정하기로 열어서 적당히 빈 곳에  
> JS_Inflator_editor.uidesc DATA "JS_Inflator_editor.uidesc"  
> background.png PNG "background.png"  
와 같이 나머지 리소스들을 다 채워넣어 준다.  

## 그러면 끝  

이제 문제 없이 컴파일과 빌드가 마무리되어야 할 것이다.  
디버깅 모드로 빌드하여 VSTGUI WYSIWYG 에디터를 사용한다면 아마 처음에는 검은 화면만 나타날 것이다.  
좌상단의 edit을 잘 클릭해서 열고, 리소스와 배경 등을 잘 추가하고 파라미터를 연결하고 저장하면 새로운 GUI로 잘 나타날 것이다.  
