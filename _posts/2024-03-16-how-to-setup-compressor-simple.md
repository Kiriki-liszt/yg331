---
title:   "컴프레서의 구조 이해와 간단한 사용 예시"
excerpt: "오인페, 마이크, 플러그인, 세팅에 대한 개론"
date:  2024-03-16 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
--- 

## 개요  

이 글은 컴프레서가 무엇인지, 구조를 이해하고 적용해보는 간단한 예시를 정리한 것입니다.  
주로 Sonnox Oxford Dynamics 매뉴얼과 UAD 홈페이지의 설명을 주로 번역하였습니다.  

## 컴프레서가 뭘까  

컴프레서는 다이나믹스 - 소리의 크기 범위, 조용한 부분과 큰 부분 사이의 크기 차이 - 를 줄이는 장치입니다.  
이때, 컴프레서가 작동하는 것이 순식간에 작동하는 것이 아니기 때문에 다양한 효과들이 발생합니다.  

* 균형잡힌 소리를 만들고, 청감 음량을 높여 청취자의 주의를 끄는 데 도움이 될 수 있습니다.  
* 다양한 소리들이 섞여있는 경우, 일체감을 줄 수 있습니다.  
* 세팅을 조절해 어택감과 음색의 밝기 등등 전체적인 '톤'이 변화합니다.  

## 컴프레서의 구조  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Overview.png){: .align-center .half-width}  

컴프레서는 기준보다 큰 소리를 일정 비율로 줄어들게 만들어 소리의 범위를 조정합니다.  
이 기능은 크게 두 가지로 나누어 볼 수 있습니다:

1. 정적 게인(level versus gain function): 항상 일정하게 작동하는 부분 - Threshold, Ratio, Knee.
2. 동적 게인(dynamic gain function) : 시간의 흐름에 영향을 받는 부분 - Attack, Release, Hold.  

### Threshold  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Threshold.png){: .align-center .half-width}  

Threshold란 컴프레서가 작동하는 '기준'으로, 데시벨(dB)로 주어집니다. 즉, 이 값보다 커질 때 소리가 줄어드는 작동(=컴프레션)이 이루어지는 것입니다.  

### Ratio  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Ratio.png){: .align-center .half-width}  

Ratio는 컴프레서가 작동할 때, 어떠한 비율로 줄어들게 할 지를 말합니다.  
예를 들어, 2:1의 Ratio 세팅은 Threshold를 넘어선 소리를 절반으로 줄일 것입니다.  
2dB만큼 넘어섰다면 1dB로 줄일 것이고, 8dB만큼 넘어섰다면 4dB로 줄일 것입니다.  

일반적으로, 3:1은 적당한 컴프레션, 5:1은 중간 정도의 컴프레션, 8:1은 강한 컴프레션, 20:1 부터는 '리미터' 영역으로 넘어갑니다.  

### Knee  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Knee.png){: .align-center .half-width}  

Knee란 컴프레서가 작동하는 영역과 작동하지 않는 영역이 만나는 지점에서, Ratio가 어떻게 변화하는지에 대한 것입니다.  
두 영역이 주드럽게 이어지면 'Soft knee', 칼같이 떨어지면 'Hard knee'라고 합니다.  

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

### Hold Time  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Hold_0.1.png){: .align-center .half-width}  
<sup class="align-center">Transient 0.1s</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Hold_0.2.png){: .align-center .half-width}  
<sup class="align-center">Transient 0.2s</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Hold_0.3.png){: .align-center .half-width}  
<sup class="align-center">Transient 0.3s</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Hold_0.4.png){: .align-center .half-width}  
<sup class="align-center">Transient 0.4s</sup>  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-03-16/Hold_0.5.png){: .align-center .half-width}  
<sup class="align-center">Transient 0.5s</sup>  

Hold는 컴프레서가 작동한 시점으로부터 Release가 작동하기까지의 시간을 말합니다.  
예를 들어, Hold가 0.3 sec로 설정되었을 때 - 큰 입력 신호가 0.3 sec보다 길게 유지되었다면 Release는 영향을 받지 않지만, 0.3 sec보다 짧게 유지되었다면 Release는 이에 영향을 받아 설정한 값보다 더 길어집니다.  
이때 Release 시간은 Hold에 영향을 받는 정도만큼 비례하여 길어집니다.  
즉, 컴프레서가 작동했던 시간이 짧을 때만 Release를 길게 하고, 이를 통해 컴프레서가 급격하게 작동하는 것을 완화하여 소리의 영향을 줄일 수 있습니다.  

## 세팅에 따른 효과  

### 정적 게인 요소(Threshold, Ratio, Knee)의 조정  

일반적으로, 컴프레서를 사용하는 목적은 '다이나믹스를 조절하는 것'과 '특징적인 효과 부여' 두 가지로 나뉩니다.  
다이나믹스를 조정하기 위해 보컬, 악기, 전체 믹스 등에 사용하는 경우, 컴프레서가 작동하고 있다는 것을 눈치채지 못 할 정도로 투명하게 사용하기 원합니다.  
반대로 특징적인 효과를 부여하기 위해서는 컴프레서를 좀 더 과장시켜 사용하여 더 두드러지게 사용합니다.  
이러한 차이를 잘 인지하기 위해서는 우리의 인식이 단순한 '볼륨의 차이' 보다는 '볼륨이 변화하는 순간'을 더 많이 듣는다는 것에 집중하여야 합니다.  

#### '가능한 한 적게' 방식  

제일 직관적인 방식으로, 대부분의 소리는 건드리지 않고 큰 부분에서만 살짝 작동하도록 하는 것입니다.  
이는 영향을 받는 부분이 적다는 심리적 이점을 가지고 있습니다.  

다음과 같이 높은 Threshold와 3~4:1 정도의 Ratio, Hard knee를 주어 제일 큰 부분들만 잡아주는 방식입니다.  
이러한 방식은 볼륨이 변화하는 순간이 급격하게 변하는 단점을 가지고 있습니다.  
이는 소리에 투명하지 않은 영향을 줄 것이고, 완화하기 위해 더 긴 Attack/Release를 사용하게 될 가능성이 높습니다.  
이 과정에서 정적 게인 요소보다 동적 게인 요소에 집중하게 될 것입니다.  
그러므로 이러한 방식은 컴프레서를 '음향 효과'로서 사용하는데에는 유리하지만, 원래 목적인 '다이나믹 제어'로서는 불리한 것입니다.  

이를 보완한 방식은 knee를 soft하게 바꿔주는 것입니다.  
이렇게 함으로서 컴프레서는 서서히 작동할 것이고, 급격한 소리의 변화를 막아줍니다.  

이 보완된 방식의 장점은 소리에 영향이 가는 것을 최소화하며 Attack/Release를 더 빠르게 작동시킬 수 있다는 점입니다.  
이는 동일한 최대 크기 조건에서도 더 많은 컴프레션을 할 수 있고, 청감 음량을 키울 수 있다는 것입니다.  
또한, 더 빠른 Attack/Release는 peak(제일 큰 소리)가 더 많이 제어되므로 이후 리미터를 작동시킬 때 조금 더 영향을 줄일 수 있습니다.  

#### '전반적으로 다' 방식  

이는 소리를 전반적으로 다 컴프레션이 걸리는 상태를 유지시켜 더 투명하게 컴프레서를 적용하는 것입니다.  
이를 통해 컴프레서가 작동하는 부분과 작동하지 않는 부분을 넘나들며 발생하는 영향을 최소화하므로 더 자연스럽다는 것입니다.  
단점은 제일 큰 소리(peak)의 제어가 약해 이후 리미터나 다른 컴프레서를 강하게 걸 가능성이 생긴다는 것입니다.  

다음과 같이 낮은 Threshold, 2:1 정도의 Ratio, soft knee를 주는 것입니다.  
또한 출력 게인을 키워주어 입출력 크기를 맞춰주었습니다.  

이 경우, 일정 이하의 크기(이 경우 -30dB)보다 작은 소리는 15dB나 키워주어 작게 들릴 수 있는 부분을 키워주었습니다.  
또한 제일 주요한 30dB 범위의 소리는 15dB 범위의 다이나믹으로 압축시켰습니다.  
이를 통해 원래 소리의 다이나믹함을 살릴 수 있습니다.  
이는 넓은 소리 크기 범위를 가지는 트랙의 청감 음량을 키우고, 자연스러운 셈여림을 남겨둘 수 있는 장점이 있습니다.  

#### 혼합 방식

상기한 두 방식을 동시에 적용해볼 수 있습니다.  

##### 최대 음량  

이는 pop이나, 팟케스트 등 음량의 변화를 원하지 않는 경우에 최대 음량을 얻기 위해 사용할 수 있는 세팅입니다.  
소리의 주요 음량 부분을 크게 키우면서도 Attack/Release를 너무 길지 않게 유지할 수 있습니다.  
Ratio는 최대(~= 리미팅), knee는 많이 soft하게(~= 15dB) 설정한 다음 원하는 청감 음량을 얻을 때 까지 Threshold를 내립니다.  

이는 소리가 커질수록 점점 더 많은 Ratio가 걸리도록 하는 것입니다.  
Ratio가 아주 많이 커지기 때문에, knee 또한 많이 soft하게 설정합니다.  

##### 최소 영향  

이는 최소한의 영향을 미치도록 낮은 Ratio(2:1)와 적당한 knee(10dB)를 주는 것입니다.  
이는 소리의 작은 부분을 키워주면서도 중간~큰 부분의 범위를 절반으로 줄여주되, 컴프레서가 톤에 미치는 영향을 최소화합니다.  
이는 Attack/Release를 짧게 줄 수 있고, 원래 소리가 가지는 다이나믹을 살릴 수 있습니다.  

### 동적 게인 요소(Attack, Release, Hold)의 조정

동적 게임 요소는 컴프레션이 작동하는 소리의 성향 자체를 크게 변화시키며, 이를 접근하는 다양한 관점이 있다.  
즉, '정답'이라 할 만한 방도는 없다.  
하지만, 원하는 소리를 얻기 위해서는 컴프레서를 사용하는 감을 잡아야 하고, 이를 돕기 위해서 기본적으로 어떤 영향을 미치는지 알아두는 것을 추천한다.  

* Attack은 어택감에 관여하여 느릴 때 더 앞에서 들리는 느낌을 주고, 빠를 때 더 뒤로 보내는 느낌을 줍니다.  

* 또한, Attack이 어택감을 조정할 때 톤을 더 단단하거나(느린 어택) 부드럽게(빠른 어택) 변화시킵니다.  

* 빠른 Attack과 빠른 Release는 새츄레이션이 저역대 위주로 발생하여 '따뜻함'을 줄 수 있습니다.  

* 빠른 Release는 조용한 구간을 더 강조할 수 있으므로 더 큰 청감 음량을 얻을 수 있습니다. 느린 Release는 그 반대로 작동할 것입니다.  

* 적당 ~ 빠른 Release는 리버브의 청감 길이를 늘릴 수 있습니다.  

* 알맞은 길이의 Release는 곡의 리듬감을 더 두드러지게 할 수 있습니다.  

다음은 도움이 될 만한 기본적인 사용법들이다.  

#### Fast as Possible Approach  

To obtain absolute maximum modulation and minimum dynamic range, the best approach is to set release times to minimum, increase the hold time just enough to the reduce LF distortion to acceptable levels, and increase the attack time just enough to allow some overshoot on percussive peaks, in order to retain some impression of programme dynamics. The appropriate level of compression can then be obtained using the threshold, ratio and soft ratio controls. The overshoots produced by the attack times can be controlled by the use of the programme limiter section.

#### Natural Dynamics Approach  

To obtain a more natural compression a good starting point is to set the attack and release controls to mid positions with hold control at minimum (this is the fixed setting of the Classic compressor style). This approach aims to match to some degree the dynamics of the ear’s response and recovery from loud sounds at relatively high sound pressure levels. Variations on these moderate settings can yield realistic results if appropriately adjusted to suit the intended reproduction levels of the programme.

#### Slow and Gentle Approach  

For level control with the least possible intrusion, set the attack and release times to the longest possible times, perhaps with the addition of the hold control to increase the release times further. This ensures that the highest levels within the programme material are controlled gently, and the gain recovery in the quiet passages is almost imperceptibly slow. This method is most effective when used in conjunction with the larger soft ratio settings, as this ensures that compression commences well before the target maximum level, providing a degree of prediction.

#### Artistic Effects  

The manipulation of timing within compression can create some very useful effects. In particular, gain overshoots produced by slow to moderate attack times can be very useful at tightening up soft percussion sounds. However, a note of caution is needed for users of workstation applications in that effects such as these may cause unexpected programme clipping that may prevent the available range of possible sounds being fully appreciated. In particular, for systems that lack overload margin between plug-ins or within their mixing structures, the extra short term peaks produced by creative compression may be prematurely clipped within the host application because essentially there is no range (headroom) to accommodate them. In this case a reduction of input levels and/or a suitable reduction of the threshold and gain make-up values may be needed to fully realise the new sound within the intended mix.

### 부록  

EQ와 컴프레서를 적용하는 순서에 따라 다른 기능이 있습니다. EQ 다음에 컴프레서를 두면 EQ로 소리를 정리하여 음역대에 에너지가 뭉친 부분이 없이 컴프레서를 통과하여 다이나믹을 컨트롤하기 쉽다는 장점이 있습니다. 컴프레서 다음에 EQ를 둔다면 소리에 영향을 주는 것이 없으므로 안정적으로 음색을 조절할 수 있습니다. 따라서 둘 중 나중에 오는 것이 더 큰 영향을 준다고 이해하시면 됩니다. 만약 익숙해지신다면 EQ->Comp->EQ의 순서로 역할을 나누어 사용하시는 것이 좋습니다.  
