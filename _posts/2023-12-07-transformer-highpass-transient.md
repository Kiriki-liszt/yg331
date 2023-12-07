---
title:   "Transformers, highpass and transient"
excerpt: "플러그인 분석"
date:  2023-12-07 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## Transformer sound and Transient  

흔히 말하는 "트랜스포머의 소리"가 무엇인지 이리저리 분석하던 중, transient에 특이한 현상이 발생하는 것을 알게 되었다.  
바로 주기를 가지고 흔들리는 attack과 release를 가지는 것이었다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/decap-atk.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/decap-rls.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/1073-atk.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/1073-rls.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/gem-atk.png){: .align-center}  

처음에는 이것이 Transformer의 사운드를 결정짓는 것인가! 하고 어떤 알고리즘을 사용해야 이런 현상이 일어나는지 열심히 찾아다녔지만, 그런 내용은 없었다.  

그러다 Airwindows에도 분명 transformer 알고리즘이 있을 거라 생각해 찾아보니 Coils가 있었다. 이를 같은 방법으로 분석해본 결과, 같은 현상이 일어나고 있는 것을 보고 알고리즘 분석에 들어갔다.  

해당 saturation 알고리즘에는 특이한 구석이 (물론 Airwindows-typical하게 특이했지만 그것 말고는) 보이지는 않았다.  
해서, transient가 아닌 frequency 분석으로 돌아가 보니 Transformer를 충실히 구현한 플러그인들은 다 Band-Limited되어 있음을 발견했다.  

## Highpass and Transient  

Oxford EQ를 가지고 Highpass, Lowpass를 걸어가며 분석해본 결과, 저러한 Transient에 영향을 미치는 부분은 Highpass였다.  
추가로 실험해본 결과, dB/oct와 cutoff freq가 transient에 미치는 영향이 비례했다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/hp-atk.png){: .align-center}  
![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-12-07/hp-rls.png){: .align-center}  

그러므로, Transformer의 특징적인 사운드 중 하나일 수 있지만, 결국 transformer는 saturation algo를 어떻게 디자인하느냐가 더 중요한 것이라 결론내렸다.  
그리고 우리가 Highpass를 걸면서 더 tight하다고 느꼈던 것은 실제로도 transient가 강조되므로 그렇게 들렸던 것이다!  
