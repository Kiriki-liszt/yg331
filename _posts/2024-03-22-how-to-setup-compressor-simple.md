---
title:   "컴프레서의 간단한 이해와 사용 예시"
excerpt: "플러그인에 대한 개론"
date:  2024-03-22 00:12:05 +0900

categories:
  - Plugin

tags:
  - VST
  - PC
--- 

## 개요  

이 글은 컴프레서가 무엇인지, 구조를 이해하고 적용해보는 간단한 예시를 정리한 것입니다.  
더 자세한 내용은 다음 [블로그 링크](https://kiriki-liszt.github.io/yg331/plugin/how-to-setup-compressor-full/)에 정리해두었습니다.  

## 컴프레서가 뭘까  

컴프레서는 다이나믹스 - 소리의 크기 범위, 조용한 부분과 큰 부분 사이의 크기 차이 - 를 줄이는 장치입니다.  
이를 사용하여 균형잡힌 소리를 만들고, 청감 음량을 높여 청취자의 주의를 끄는 데 도움이 될 수 있습니다.  
또한, 컴프레서가 작동하는 방식에 따라 어택감과 음색의 밝기 등등 전체적인 '톤'이 변화합니다.  

## 컴프레서의 작동 방식  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Overview.png){: .align-center .half-width}  

컴프레서는 기준보다 큰 소리를 일정 비율로 줄어들게 만들어 소리의 범위를 조정합니다.  

### Threshold(기준점)  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Threshold.png){: .align-center .half-width}  

Threshold란 컴프레서가 작동하는 '기준'으로, 데시벨(dB)로 주어집니다.  
즉, 이 값보다 커질 때 소리가 줄어드는 작동(=컴프레션)이 이루어지는 것입니다.  

### Ratio(압축 비율)  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Ratio.png){: .align-center .half-width}  

Ratio는 컴프레서가 작동할 때, 어떠한 비율로 줄어들게 할 지를 말합니다.  
예를 들어, 2:1의 Ratio 세팅은 Threshold를 넘어선 소리를 절반으로 줄일 것입니다.  
2dB만큼 넘어섰다면 1dB로 줄일 것이고, 8dB만큼 넘어섰다면 4dB로 줄일 것입니다.  

일반적으로, 2~3:1은 적당한 컴프레션, 5:1은 중간 정도의 컴프레션, 8:1은 강한 컴프레션, 20:1 부터는 '리미터' 영역으로 넘어갑니다.  

### Attack Time  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Atk_short.png){: .align-center .half-width}  
<sup class="align-center">Short Attack(1ms)</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Atk_mid.png){: .align-center .half-width}  
<sup class="align-center">Medium Attack(10ms)</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Atk_long.png){: .align-center .half-width}  
<sup class="align-center">Long Attack(50ms)</sup>  

Attack은 입력 소리가 Threshold를 넘어설 때, 컴프레서가 완전히 작동할 때까지 걸리는 시간을 말합니다.  
일반적으로 '빠른' 세팅은 20 ~ 800 us(1176, FET 타입), '느린' 세팅은 10 ~ 100 ms(LA-2a, Opto 타입) 입니다.  

이 값을 조정하는 것으로 '펀치감' 이라 느끼는 트랜지언트 부분을 더 부각하거나(느린 어택), 반대로 줄이거나(빠른 어택) 할 수 있습니다.  

### Release Time  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Rls_short.png){: .align-center .half-width}  
<sup class="align-center">Short Release(minimun, 5ms)</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Rls_mid.png){: .align-center .half-width}  
<sup class="align-center">Medium Release(35ms)</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Rls_long.png){: .align-center .half-width}  
<sup class="align-center">Long Release(0.1sec)</sup>  

Release는 입력 소리가 다시 Threshold보다 작아질 때, 원래대로 돌아오는데 걸리는 시간을 말합니다.  
이 값은 Attack보다 더 긴 시간을 가지며, 짧게는 40 ~ 60 ms 부터 길게는 2 ~ 5 s 까지 걸립니다.  
사진의 예시는 보여주기 위한 것으로, 사실 다 짧습니다.  

Release는 가능한 한 짧게, '울렁'거리는 것이 들리지 않도록 세팅하는 것이 추천됩니다.  
이러한 울렁거림은 저음 영역에서 나타나며, 주의 깊게 들어야 합니다.  

## 세팅에 따른 효과  

컴프레서가 작동하는 소리를 드딕 위해서는, 단순한 '볼륨의 차이' 보다는 '볼륨이 변화하는 순간'에 집중하여야 합니다.  

### '가능한 한 적게' 방식  

제일 직관적인 방식으로, 대부분의 소리는 건드리지 않고 큰 부분에서만 살짝 작동하도록 하는 것입니다.  
이는 영향을 받는 부분이 적다는 심리적 이점을 가지고 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Comp_2.png){: .align-center .half-width}  

비교적 높은 Threshold와 4:1 정도의 Ratio, medium knee.  

### '전반적으로 다' 방식  

이는 소리를 전반적으로 다 컴프레션이 걸리는 상태를 유지시켜 더 투명하게 컴프레서를 적용하는 것입니다.  
이를 통해 컴프레서가 작동하는 부분과 작동하지 않는 부분을 넘나들며 발생하는 영향을 최소화하므로 더 자연스럽다는 것입니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Comp_3.png){: .align-center .half-width}  

낮은 Threshold, 2:1 정도의 Ratio, softer knee.  

### 최대 음압  

소리가 커질수록 점점 더 많은 Ratio가 걸리도록 하여, pop이나 팟케스트 등 음량의 변화를 원하지 않는 경우에 최대 음압을 얻기 위해 사용할 수 있는 세팅입니다.  
소리의 주요 음량 부분을 크게 키우면서도 Attack/Release를 너무 길지 않게 유지할 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Comp_4.png){: .align-center .half-width}  

Ratio는 최대, knee는 많이 soft하게(>= 15dB) 설정한 다음 원하는 청감 음량을 얻을 때 까지 Threshold를 내립니다.  

### Attack과 Release의 세팅  

이 두가지 요소는 컴프레션이 작동하는 소리의 성향 자체를 크게 변화시키며, 이를 접근하는 다양한 관점이 있습니다.  
즉, '정답'이라 할 만한 세팅은 없습니다.  
하지만 원하는 소리를 얻기 위해서는 컴프레서를 사용하는 감을 잡아야 하고, 이를 돕기 위해서 기본적으로 어떤 영향을 미치는지 알아두는 것을 추천합니다.  

* Attack은 어택감에 관여하여 느릴 때 더 앞에서 들리는 느낌을 주고, 빠를 때 더 뒤로 보내는 느낌을 줍니다.  

* 또한, Attack이 어택감을 조정할 때 톤을 더 단단하거나(느린 어택) 부드럽게(빠른 어택) 변화시킵니다.  

* 빠른 Attack과 빠른 Release는 새츄레이션이 저역대 위주로 발생하여 '따뜻함'을 줄 수 있습니다.  

* 빠른 Release는 조용한 구간을 더 강조할 수 있으므로 더 큰 청감 음량을 얻을 수 있습니다. 느린 Release는 그 반대로 작동할 것입니다.  

* 적당 ~ 빠른 Release는 리버브의 청감 길이를 늘릴 수 있습니다.  

* 알맞은 길이의 Release는 곡의 리듬감을 더 두드러지게 할 수 있습니다.  

제일 무난한 시작점을 골라보자면, Attack과 Release를 중간 정도(Atk : 5.2ms, Rls : 0.127s)에서부터 시작하는 것입니다.  
