---
title:   "WAVES V-EQ saturation"
excerpt: "V-EQ의 THD"
date:  2022-08-11 00:12:05 +0900

categories:
  - VST
  - EQ

tags:
  - analog
---

스튜디오의 엔지니어분이 믹스하시는걸 보거나 유명한 해외 팝 세션들을 받아 열어보면 생각보다 보편적인 플러그인들이 걸려 있을 때가 있다.  
그렇게 알게 된 게 WAVES의 V-EQ다.  

## WAVES V-EQ  
  
![WAVES veq]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-11-veq-saturation/WAVES V-EQ4.png){: .align-center}  

이 시리즈는 NEVE EQ의 복각 플러그인으로 V-EQ3는 1073/1066 모듈을, V-EQ4는 1081 모듈을 복각하였다.  
두 EQ 모두 Discrete한 EQ로 설정할 수 있는 주파수가 고정되어 있다.  
이렇게 주파수가 고정되어 있어 믹스나 녹음 시 빠른 결정에 도움을 준다.  

주로 사용하는 것은 V-EQ4로 보컬에서 1000, 1200Hz를 조금 깍고 10kHz high shelf를 살짝 올려주는데 쓴다.  

V-EQ를 알게 되고 이러한 용도로 쓰기에 잘 맞다는 걸 알고 나서 한동안은 계속 이거만 썼던 것 같다.  

![WAVES veq]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-11-veq-saturation/V-EQ4 100 thd.png){: .align-center}  
![WAVES veq]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2022-08-11-veq-saturation/V-EQ4 1000 thd.png){: .align-center}  

하지만 최근 보컬 믹스를 하는데 소리가 너무 금방금방 saturation되는 걸 느꼈다.  
그래서 걸려있던 플러그인들의 배음을 전부 보았더니 이 V-EQ에서 saturation이 일어나는걸 발견했다.  
심지어 analog 버튼을 끈 상태인데도 발생하고 있다.  

신기해서 매뉴얼을 읽어보니 아날로그 장비의 특성을 모두 살리기 위해 해당 NEVE 모듈에서 발생하는 모든 배음 특성을 복각했다는 것을 찾았다.  
즉 analog 버튼을 끈 상태에도 EQ logic 자체에 배음이 걸린다는 것이다.  

물론 정도가 크지 않아 전체 보컬 체인에서 엄청난 saturation을 발생하는 원인은 아니었지만 플러그인의 특성을 잘 알아보는 계기를 주었다.  
이후 세션을 더 분석해보니 보컬이 크게 지를 때 CLA-2A에서 생각보다 많은 saturation이 걸리고 있었다.  
결국 그 부분만 오토메이션과 클립게인을 걸어서 해결했다.  
