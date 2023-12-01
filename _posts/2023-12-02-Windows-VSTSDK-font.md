---
title:   "VSTSDK 사용 시 Windows에서 .rc 파일에 폰트 추가하고 custom font로 불러오기"
excerpt: "플러그인을 만들어보자!"
date:  2023-12-02 00:12:05 +0900

categories:
  - Production

tags:
  - VST
  - PC
---

## 시작하기  

VSTSDK 3.7.9, 왼도우 10, VS2022 community를 사용했다.  

## 폰트의 호출  

> uidescrtion -> uinode -> cfont -> win32factory -> D2Dfont  

폰트가 사용될 때 다음과 같은 경로로 호출된다.  
그리고 기존 customfont가 추가되는 것은 win32factory의 "Win32Factory::createFont"가 "makeOwned < D2DFont > "를 통해 D2DDont가 construst될 때이다.  

## 기존의 customfont  

VSTGUI 4.9 이상부터는 Resources/Fonts 폴더에 존재하는 폰트들을 모두 읽어 fontcollection으로 등록하는 구현이 추가되어 있다.  
이러한 방식은 macOS에서도 사용할 수 있는 cross-platfrom 기능이지만, 나는 windows 특정 dll 단일 파일로 빌드하기 때문에 사용할 수 없다.  

## 참고 - microsoft/Windows-classic-samples/Samples/DirectWriteCustomFontSets  

<https://learn.microsoft.com/en-us/windows/win32/directwrite/custom-font-sets-win10>  
<https://github.com/microsoft/Windows-classic-samples/tree/main/Samples/DirectWriteCustomFontSets>  

두 페이지를 잘 읽어보고 적용해보자.  

## 구현 @ D2Dfont.cpp  

```c++
namespace VSTGUI {
namespace D2DFontPrivate {

//-----------------------------------------------------------------------------
struct CustomFonts
{
#if VSTGUI_WIN32_CUSTOMFONT_SUPPORT
  struct MemoryFontInfo
  {
    HGLOBAL fontData;
    uint32_t fontDataSize;
  };

  void AddFontResourceToVector (wchar_t const* resourceName)
  {
    HRSRC hFontResource = FindResource (GetInstance (), resourceName, MAKEINTRESOURCE(RT_RCDATA));

    if (hFontResource == nullptr)
      return;

    uint32_t binaryFontDataSize = SizeofResource (GetInstance (), hFontResource);
    HGLOBAL hFontResource_Loaded = LoadResource (GetInstance (), hFontResource);
    if (hFontResource_Loaded == nullptr)
      return;

    void* binaryFontData = LockResource (hFontResource_Loaded);
    if (binaryFontData != nullptr)
    {
      MemoryFontInfo fontInfo = {binaryFontData, binaryFontDataSize};
      m_appFontResources.push_back (fontInfo);
    }
  };

  ~CustomFonts ()
  {
    if (m_inMemoryFontFileLoader.get () != nullptr)
      m_dwriteFactory5->UnregisterFontFileLoader (m_inMemoryFontFileLoader.get ());
  } 

  CustomFonts ()
  {
    auto factory = getDWriteFactory ();

    if (!factory ||
      FAILED (factory->QueryInterface<IDWriteFactory5> (m_dwriteFactory5.adoptPtr ())))
      return;

    m_dwriteFactory5->CreateInMemoryFontFileLoader (m_inMemoryFontFileLoader.adoptPtr ());
    m_dwriteFactory5->RegisterFontFileLoader (m_inMemoryFontFileLoader.get ());

    COM::Ptr<IDWriteFontSetBuilder1> fontSetBuilder;
    m_dwriteFactory5->CreateFontSetBuilder (fontSetBuilder.adoptPtr ());

    // your font  
    AddFontResourceToVector (L"PretendardRegular");

    for (uint32_t fontIndex = 0; fontIndex < m_appFontResources.size (); fontIndex++)
    {
      MemoryFontInfo fontInfo = m_appFontResources[fontIndex];

      COM::Ptr<IDWriteFontFile> fontFileReference;

      m_inMemoryFontFileLoader->CreateInMemoryFontFileReference (
        m_dwriteFactory5.get (),
        fontInfo.fontData,
        fontInfo.fontDataSize,
        m_inMemoryFontFileLoader.get (),
        fontFileReference.adoptPtr());


      fontSetBuilder->AddFontFile (fontFileReference.get ());
    }

    fontSetBuilder->CreateFontSet (fontSet.adoptPtr ());
    m_dwriteFactory5->CreateFontCollectionFromFontSet (fontSet.get (),
    fontCollection.adoptPtr ());
    return;
  }

private:
  COM::Ptr<IDWriteInMemoryFontFileLoader> m_inMemoryFontFileLoader; 
  COM::Ptr<IDWriteFactory5> m_dwriteFactory5;
  COM::Ptr<IDWriteFontSet> fontSet;
  COM::Ptr<IDWriteFontCollection1> fontCollection;

  std::vector<MemoryFontInfo> m_appFontResources;

#else
//~
#endif
};
}
}
```  

## 구현 @ win32resource  

```c
#include <windows.h>
#include "../source/version.h"

#define APSTUDIO_READONLY_SYMBOLS

your_editor.uidesc DATA "your_editor.uidesc"

PretendardRegular RCDATA "Pretendard-Regular.ttf"

//~~~
```  

## 사용  

.rc파일에 RCDATA로 등록해주고, 이름을 지정해준 다음 D2DFont.cpp에서 AddFontResourceToVector 해주면 된다.  
물론 다른 폰트, 더 많은 폰트를 사용한다면 다 AddFontResourceToVector 해준다.  
