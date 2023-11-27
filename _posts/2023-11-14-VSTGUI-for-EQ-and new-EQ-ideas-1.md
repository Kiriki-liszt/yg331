---
title:   "VSTGUI와 EQ curve, 그리고 새로운 EQ - 1"
excerpt: "플러그인 이야기"
date:  2023-11-14 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 원하는 것  

VSTSDK + VSTGUI만을 사용해 플러그인의 EQ를 표현하고자 한다.  
이는 새로운 EQ를 만드려는데 있으면 좋을 것 같기 때문이다.  

## 환경 세팅  

VSTSDK 3.7.9, Windows 10, VS2023 community에서 실행한다.  

## VSTGUI 메소드 - CGraphicsPath  

``` c++
void MyView::draw(VSTGUI::CDrawContext* pContext)
{
  VSTGUI::CGraphicsPath* path = pContext->createGraphicsPath();
  if (path)
  {
    VSTGUI::CRect r(getViewSize());
    VSTGUI::CCoord y_mid = r.bottom - (r.getHeight() / 2.0);
    path->beginSubpath(VSTGUI::CPoint(r.left, y_mid));
    double MAX_FREQ = 20000.0;
    double MIN_FREQ = 10.0;
    double FREQ_LOG_MAX = log(MAX_FREQ / MIN_FREQ);
    double DB_EQ_RANGE = 20.0;
    for (int x = 0; x <= r.getWidth(); x++) {
      double tmp = MIN_FREQ * exp(FREQ_LOG_MAX * x / (r.getWidth()));
      double freq = max(min(tmp, MAX_FREQ), MIN_FREQ);
      double db = 20 * log10(calc(freq));
      double m = 1.0 - (((db / DB_EQ_RANGE) / 2) + 0.5);
      double scy = m * r.getHeight();
      path->addLine(VSTGUI::CPoint(r.left + x, r.top + scy));
    }
    path->addLine(r.right, r.bottom);
    path->addLine(r.left, r.bottom);
    path->addLine(r.left, y_mid);
    path->closeSubpath();

    pContext->setFrameColor(VSTGUI::kBlackCColor);
    pContext->setDrawMode(VSTGUI::kAntiAliasing);
    pContext->setLineWidth(1);
    const VSTGUI::CCoord kDefaultOnOffDashLength[] = { 1, 2 };
    pContext->setLineStyle(VSTGUI::kLineSolid); 

    pContext->drawGraphicsPath(path, VSTGUI::CDrawContext::kPathStroked);
    path->forget();
  }
}
```

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-14/screenshot.png){: .align-center}  

Point-to-Point나 Triangle보다 CGraphicsPath를 사용했다.  

## 원하는 EQ 디자인  

최근에 Ozone 11 EQ가 무료로 풀려서 무료 EQ에 대한 수요가 줄어들었겠지만, Oxford EQ 스타일의 EQ를 하나 만들어보고 싶었다.  
그리고 Maag 스타일의 Air Band 노브는 별도로 추가하고 싶다.  
아니면 GML(AMEK), Neve, Pultec, API 등의 커브를 사용해볼 수 있는 옵션도 재미있을 것 같다.  
SSL은 Oxford와 겹친다고 보고 생략.  
