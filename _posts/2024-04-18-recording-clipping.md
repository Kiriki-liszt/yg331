---
title:   "보컬 녹음 시 주의점 - 클리핑, 팝필터"
excerpt: "녹음하기"
date:  2024-04-18 00:12:05 +0900

categories:
  - DAW

tags:
  - VST
  - PC
--- 

## 개요  

이 내용은 보컬 등의 녹음 시, 너무 큰 소리로 녹음되어 클리핑이 나는 것과 팝필터를 사용하지 않아 과도한 파열음이 나는 것을 피하는 것에 대한 이야기입니다.  

## 1. 클리핑이란?  

소리가 한계치보다 더 커져, 파형이 잘려버리는 현상을 말합니다.  
이는 소리에 강한 배음 성분을 생성하기 때문에 적당한 정도는 음압에 도움이 되지만, 적절하지 못한 경우 '찢어지는 소리'가 되어 더 안 좋은 결과를 얻습니다.  
그 예시가 바로 보컬 등의 녹음에서 발생하는 것입니다.  
이는 플러그인으로 어느정도 복구를 시도할 수 있지만, 말 그대로 어느정도 이며 발라드와 같이 잔잔한 곡에서는 지저분하게 티가 납니다.  
그러므로, 나중에 음악적인 의도를 가지고 사용할지라도 녹음 자체는 깨끗하게 받아야 합니다.  

이러한 클리핑은 귀로도 듣고 판단할 수 있지만, 제일 먼저 파형으로도 알아낼 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-04-18/Clipped.png){: .align-center .half-width}  

이와 같이 파형이 자로 잰 듯 잘려있는 것이 바로 클리핑이 된 것입니다.  
iZotope RX를 사용해 다음과 같이 파형을 복구해볼 수 있지만, 이미 생성된 찢어지는 배음은 쉽게 사라지지 않습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-04-18/De-clip.png){: .align-center .half-width}  

이를 막기 위해서는 우선 녹음할 때 마이크와의 거리, 오디오 인터페이스의 게인을 잘 확인하셔야 합니다.  

보컬의 경우, 컨덴서 마이크과의 거리는 보통 15cm로 잡습니다.  
또한 가까운 벽을 등지고, 넓은 곳을 향한 채로 녹음하는 것이 조금이나마 더 좋습니다.  
오디오 인터페이스의 게인은 아예 주황색 불빛이 들어오지 않을 정도로 작게 녹음하시면 되겠습니다.  

또한, 놓치기 쉬운 부분으로 DAW로 녹음한 것을 파일로 만들 때 녹음된 소리가 작다고 왕창 키운 채로 파일로 만들어버려도 클리핑이 일어납니다.  
녹음된 소리가 MR에 비해 작다면, MR을 줄입시다.  

## 2. 팝필터란?

![pop-filter](https://d2pucgucjvdva3.cloudfront.net/sites/default/files/styles/max_1300x1300/public/news/2020-10/blog_shockmount_popfilter_img_5324.jpg){: .align-center .half-width}  

녹음 시, 마이크 앞에서 과도한 파열음을 막아주는 도구입니다.  
이는 파열음과 바람소리를 막아주어 더 안정적인 보컬을 얻을 수 있습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-04-18/Plosive.png){: .align-center .half-width}  

이와 같이 파열음은 과도한 저역대로 나타나게 됩니다.  

이 또한 믹싱 과정에서 해당 부분만 잘라내고 플러그인으로 처리한 후, 다시 앞뒤를 크로스페이드해서 처리할 수 있지만, 처음부터 팝필터를 사용하는 것이 마이크에도 더 좋습니다.  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2024-04-18/De-Plosive.png){: .align-center .half-width}  

## 결론  

이런 후처리(포스트 프로세싱) 과정은 어쩔 수 없이 원 음질의 손상을 가져옵니다.  
복구할 수 없는 부분도 있구요.  
그러므로 처음부터 깔끔하게 받는것이 제일 중요합니다.  

## 읽을거리  

보컬 녹음에 도움이 될만한 자료가 있어 첨부합니다.  

[보컬 마이킹 1편 - ON AXIS / OFF AXIS](https://sionkimmusic.com/article/?mod=document&uid=41&pageid=1)  
[보컬 마이킹 2편 - 보컬과 마이크의 거리](https://sionkimmusic.com/article/?mod=document&uid=42&pageid=1)  
[보컬 마이킹 3편 - 녹음 부스에서 마이크와 보컬의 위치](https://sionkimmusic.com/article/?mod=document&uid=43&pageid=1)  
