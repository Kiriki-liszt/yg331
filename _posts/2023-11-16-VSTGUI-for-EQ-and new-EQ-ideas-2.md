---
title:   "VSTGUI와 EQ curve, 그리고 새로운 EQ - 2"
excerpt: "플러그인 이야기"
date:  2023-11-16 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

![]({{ site.url }}{{ site.baseurl }}/assets/images/post_images/2023-11-16/screenshot.png){: .align-center}  

## VSTGUI - Custom View  

``` c++
// Header

namespace VSTGUI {
  
  class MyView : public CView
        , public Steinberg::FObject
        , public DelegationController
  {
  public:
    MyView(const VSTGUI::CRect& size, Steinberg::Vst::EditController* editController = nullptr);
    ~MyView();

    // --- CView methods ---
    void draw(CDrawContext* pContext) override;
    //CMouseEventResult onMouseDown(CPoint& where, const CButtonState& buttons) override;
    //CMouseEventResult onMouseUp(CPoint& where, const CButtonState& buttons) override;
    //CMouseEventResult onMouseMoved(CPoint& where, const CButtonState& buttons) override;

    CLASS_METHODS(MyView, CView)

  private:

    // --- IDependent (FObject) methods ---

    void PLUGIN_API update(Steinberg::FUnknown* changedUnknown, Steinberg::int32 message) override;

    // --- attributes ---

    Steinberg::Vst::EditController* editController;

    Steinberg::Vst::Parameter* uiParamBand1_dB;
    Steinberg::Vst::Parameter* uiParamBand1_Hz;
    Steinberg::Vst::Parameter* uiParamBand1_Q;

    Steinberg::Vst::ParamValue fBand1_dB = 0.5;
    Steinberg::Vst::ParamValue fBand1_Hz = 0.5;
    Steinberg::Vst::ParamValue fBand1_Q = 0.5;

    double calc(double freq);
    yg331::SVF_ Band1;
  };
}


namespace yg331 {
//------------------------------------------------------------------------
//  GUI_Controller
//------------------------------------------------------------------------
class GUI_Controller : public Steinberg::Vst::EditControllerEx1, public VSTGUI::VST3EditorDelegate
{
public:
//------------------------------------------------------------------------
  GUI_Controller () = default;
  ~GUI_Controller () SMTG_OVERRIDE = default;

// ~~~

VSTGUI::CView* createCustomView (VSTGUI::UTF8StringPtr name, const VSTGUI::UIAttributes& attributes,
                 const VSTGUI::IUIDescription* description, VSTGUI::VST3Editor* editor) override
{
  if (VSTGUI::UTF8StringView(name) == "MyView")
  {
    VSTGUI::CRect size(VSTGUI::CPoint(10, 10), VSTGUI::CPoint(400, 150));
    myView = new VSTGUI::MyView(size, this);
    return myView;
  }
  return nullptr;
}

//~~~
protected:
  VSTGUI::MyView* myView = nullptr;
}
}
```

헤더에서는 EQ curve를 표시할 MyView를 선언하고, GUI_Controller(플러그인의 최상위 컨트롤러)에 public VSTGUI::VST3EditorDelegate를 상속한다.  
그리고 createCustomView를 override하여 위에서 선언한 MyView 호출시 생성한다.  

``` c++
// controller
namespace VSTGUI {
  MyView::MyView(const VSTGUI::CRect& size, Steinberg::Vst::EditController* editController)
    : DelegationController(nullptr)
    , CView(size) 
    , editController(editController)
  {
    // retrieve the parameter that we are interested in from controller
    uiParamBand1_dB = editController->getParameterObject(kParamBand1_dB);
    uiParamBand1_Hz = editController->getParameterObject(kParamBand1_Hz);
    uiParamBand1_Q  = editController->getParameterObject(kParamBand1_Q );

    // listen to these parameters (parameter changes will trigger update() )
    if (uiParamBand1_dB) uiParamBand1_dB->addDependent(this);
    if (uiParamBand1_Hz) uiParamBand1_Hz->addDependent(this);
    if (uiParamBand1_Q ) uiParamBand1_Q ->addDependent(this);
  }

  MyView::~MyView()
  {
    if (uiParamBand1_dB) uiParamBand1_dB->removeDependent(this);
    if (uiParamBand1_Hz) uiParamBand1_Hz->removeDependent(this);
    if (uiParamBand1_Q)  uiParamBand1_Q ->removeDependent(this);
  }

  // ...
  /*
  CMouseEventResult MyView::onMouseDown(CPoint& where, const CButtonState& buttons)
  {
    // ...
    // editController->beginEdit(tag);
    // ...
  }


  CMouseEventResult MyView::onMouseMoved(CPoint& where, const CButtonState& buttons)
  {
    // ...
    // editController->performEdit (tag, value);
    // editController->setParamNormalized (tag, value);
    // ...
  }

  CMouseEventResult MyView::onMouseUp(CPoint& where, const CButtonState& buttons)
  {
    // ...
     // editController->endEdit(tag);
     // ...

  }
  */
  void PLUGIN_API MyView::update(Steinberg::FUnknown* changedUnknown,
    Steinberg::int32 message)
  {
    // if a parameter value is changed (by host or by another control) this
    // method is called

    auto* p = Steinberg::FCast<Steinberg::Vst::Parameter>(changedUnknown);
    if (p)
    {
      if (message == kChanged)
      {
        // update local parameter value and draw()
        switch (p->getInfo().id) {
        case kParamBand1_dB:
          fBand1_dB = p->getNormalized();
          fBand1_dB = p->toPlain(fBand1_dB);
          setDirty(true);
          break;
        case kParamBand1_Hz:
          fBand1_Hz = p->getNormalized();
          fBand1_Hz = p->toPlain(fBand1_Hz);
          setDirty(true);
          break;
        case kParamBand1_Q:
          fBand1_Q  = p->getNormalized();
          fBand1_Q  = p->toPlain(fBand1_Q );
          setDirty(true);
          break;
        default:
          break;
        }
      }
      else if (message == kWillDestroy)
      {
        // stop listening to parameter changes
        if (uiParamBand1_dB) uiParamBand1_dB->removeDependent(this);
        if (uiParamBand1_Hz) uiParamBand1_Hz->removeDependent(this);
        if (uiParamBand1_Q ) uiParamBand1_Q ->removeDependent(this);
        uiParamBand1_dB = nullptr;
        uiParamBand1_Hz = nullptr;
        uiParamBand1_Q  = nullptr;
      }
    }
  }
}
```

플러그인의 controller에서 생성자와 update를 통해 parameter의 변경을 받아 저장한다.  
이후 각자의 방법으로 IIR의 FR을 얻어내면 된다.  
나는 SVF 필터를 사용하여 IIR을 얻으므로, andy cytomic의 paper들을 주로 참고하였다.  

``` uidesc
"CView": {
  "attributes": {
    "class": "CView",
    "custom-view-name": "MyView",
    "mouse-enabled": "true",
    "opacity": "1",
    "transparent": "false",
    "uidesc-label": "EQ Curve view",
    "wants-focus": "false"
  }
}
```

VSTGUI의 .uidesc 파일에서 다음과 같이 custom-view-name을 설정해주면 된다.  
