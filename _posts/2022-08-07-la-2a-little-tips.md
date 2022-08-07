---
title:   "[VST] LA-2A 컴프레서와 관련된 작은 팁"
excerpt: ""
date:  2022-08-07 12:00:00

classes: wide

header:
  teaser: # "https://farm5.staticflickr.com/4076/4940499208_b79b77fb0a_z.jpg"
  video:
    id: # -PVofD2A9t8
    provider: # youtube

categories:
  - VST
  - compressor

tags:
  - compressor

last_modified_at: # 2019-04-13T08:06:00-05:00 YYYY-MM-DD HH:MM:SS +/-TTTT : hours, minutes, seconds, and timezone offset are optional.

---

# LA-2A

보컬에 컴프레션이 필요할 때 가장 먼저 생각나는 컴프레서가 두 개 있다면 그건 아마 LA-2A와 1176일 것이다.  
나도 처음 믹싱을 배울 때 가장 먼저 접했던 컴프레서들이고, 매뉴얼에 쓰여진 특성들을 읽어보고 이해했다 생각했다. 하지만 몇 년 동안 컴프레서들과 싸우다 보니 점점 알게 되는 것들이 늘어나고 다시 매뉴얼을 보니 뒤늦게 깨닫는 것들이 있었다.  
이 포스트는 두 컴프레서들의 이러한 부분들에 대해 정리해보려 한다.  

LA-2A 

이 컴프레서는 다이나믹을 제어하기 위해 광학소자를 사용하고, 컴프레서의 작동 또한 이 소자의 물리적인 특성에 영향을 받는다.  
LA-2A만의 두 특징 중 하나는 바로 입력에 따라 어택과 릴리즈가 달라진다는 것이다.  

우선 한가지 – LA-2A는 입력 신호의 주파수(음역대)에 따라 작동점(Threshold)과 비율(Ratio)이 다르다. 

사진

https://www.uaudio.de/webzine/2004/february/index2.html 에서 가져온 사진과 입출력 비율을 맞춘 그림이다.  
이로부터 알 수 있듯이 Soft knee와 평균적으로 4:1의 Ratio를 가지고 있지만 저음에서는 3.3:1, 고음에서는 대략 5.5:1까지 Ratio가 높아진다.  
이러한 비선형적 반응이 이 LA-2A만의 특징을 나타낸다.  

또 다른 LA-2A의 특징은 입력에 따라 어택과 릴리즈 시간이 달라지는 것이다. 어택 시간은 평균적으로 10ms를 가지지만 릴리즈 시간은 이보다 조금 더 복잡하다.  
릴리즈 시간의 경우 50% 지점까지 60ms를 가지지만 완전한 컴프레션의 종료까지는 1에서 15초까지 길어진다. 즉 LA-2A의 릴리즈 타임은 서로 다른 두 개의 릴리즈가 복합적으로 나타난다 생각할 수 있다. 이는 광학 소자의 물리적인 특성 때문에 나타난다. 이 소자는 컴프레서가 오래 혹은 강하게 걸릴 경우 릴리즈 시간이 늘어난다. 이러한 입력 신호의 성격에 따라 달라지는 특성을 ‘Program dependent’라고 한다. 
