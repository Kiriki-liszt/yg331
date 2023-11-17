---
title:   "VSTGUI와 EQ curve, 그리고 새로운 EQ - 3"
excerpt: "플러그인 이야기"
date:  2023-11-18 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-18/main.png){: .align-center}  

## VSTGUI - WYSIWYG  

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-18/wysiwyg.png){: .align-center}  

보기 좋게 장 정리하면 된다.  
dB의 표기와 각 Band의 파라미터들을 하나의 컨테이너에 담아서 관리하기 쉽게 했다.  

## VSTGUI - draw  

``` C++
void MyView::draw(VSTGUI::CDrawContext* pContext)
{
 pContext->setLineWidth(1);
 pContext->setFillColor(VSTGUI::CColor(50, 50, 95, 255));
 pContext->setFrameColor(VSTGUI::CColor(0, 0, 0, 255)); // black borders
 pContext->drawRect(getViewSize(), VSTGUI::kDrawFilledAndStroked);

 double MAX_FREQ = 22000.0;
 double MIN_FREQ = 10.0;
 double FREQ_LOG_MAX = log(MAX_FREQ / MIN_FREQ);
 double DB_EQ_RANGE = 15.0;

 {
  VSTGUI::CRect r(getViewSize());
  pContext->setFrameColor(VSTGUI::CColor(255, 255, 255, 55));
  for (int x = 2; x < 10; x++) {
   VSTGUI::CCoord Hz_10 = r.getWidth() * log(10.0 * x / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_10, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_10, r.top);
   pContext->drawLine(_p1, _p2);
  }
  for (int x = 2; x < 10; x++) {
   VSTGUI::CCoord Hz_100 = r.getWidth() * log(100.0 * x / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_100, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_100, r.top);
   pContext->drawLine(_p1, _p2);
  }
  for (int x = 2; x < 10; x++) {
   VSTGUI::CCoord Hz_1000 = r.getWidth() * log(1000.0 * x / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_1000, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_1000, r.top);
   pContext->drawLine(_p1, _p2);
  }
   
  for (int x = 2; x < 3; x++) {
   VSTGUI::CCoord Hz_10000 = r.getWidth() * log(10000.0 * x / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_10000, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_10000, r.top);
   pContext->drawLine(_p1, _p2);
  }
   
  pContext->setFrameColor(VSTGUI::CColor(255, 255, 255, 155));
  {
   VSTGUI::CCoord Hz_100 = r.getWidth() * log(100.0 / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_100, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_100, r.top);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord Hz_1000 = r.getWidth() * log(1000.0 / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_1000, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_1000, r.top);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord Hz_10000 = r.getWidth() * log(10000.0 / MIN_FREQ) / FREQ_LOG_MAX;
   const VSTGUI::CPoint _p1(r.left + Hz_10000, r.bottom);
   const VSTGUI::CPoint _p2(r.left + Hz_10000, r.top);
   pContext->drawLine(_p1, _p2);
  }
 }

 {
  VSTGUI::CRect r(getViewSize());
  pContext->setFrameColor(VSTGUI::CColor(255, 255, 255, 55));
  {
   VSTGUI::CCoord dB_p15 = r.getHeight() * (1.0 - (((-15.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_p15);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_p15);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord dB_p10 = r.getHeight() * (1.0 - (((-10.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_p10);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_p10);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord dB_p5 = r.getHeight() * (1.0 - (((-5.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_p5);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_p5);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord dB_0 = r.getHeight() * (1.0 - (((.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_0);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_0);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord dB_m5 = r.getHeight() * (1.0 - (((5.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_m5);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_m5);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord dB_m10 = r.getHeight() * (1.0 - (((10.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_m10);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_m10);
   pContext->drawLine(_p1, _p2);
  }
  {
   VSTGUI::CCoord dB_m15 = r.getHeight() * (1.0 - (((15.0 / DB_EQ_RANGE) / 2) + 0.5));
   const VSTGUI::CPoint _p1(r.left, r.bottom - dB_m15);
   const VSTGUI::CPoint _p2(r.right, r.bottom - dB_m15);
   pContext->drawLine(_p1, _p2);
  }
 }

// ~~~

}
```

view의 draw에서 dB선과 Hz선을 그려주었다.  
