# UI

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [설치](#설치)
* [스펙](#스펙)
* [Components](#components)
* [Release notes](./ReleaseNotes.md)


## 개요

[Unity UI](https://docs.unity3d.com/Manual/com.unity.ugui.html)를 보다 효율적으로 사용할 수 있는 컴포넌트 제공

## 설치

1. [Game Package Manger 설치](https://assetstore.unity.com/packages/tools/utilities/game-package-manager-147711)
2. 실행 : [Unity Menu > Tools > GPM > Manager](https://github.com/nhn/gpm.unity#%EC%8B%A4%ED%96%89)
3. 서비스 설치 : UI

## 스펙

### Unity 지원 버전

* 2019.4.0 이상

#### NameSpace
```cs
using Gpm.UI;
```

## Components

|Component| 설명 |
| --- | --- |
| [Infinite Scroll](InfiniteScroll/README.md) | 스크롤 사각 영역(Scroll Rect(Scroll View))을 사용할 때 뷰포트(Viewport) 크기에 맞게 아이템을 생성해 재사용할 수 있는 컴포넌트입니다. |
| [Tab Control](TabControl/README.md) | UI에서 자주 사용하는 Tab과 TabPage를 제어하는 컴포넌트입니다. |
| [Multi Layout](MultiLayout/README.md) | UI 컴포넌트의 RectTransform 정보를 여러 개의 레이아웃으로 설정해 해상도, 화면 방향 등에 대응할 수 있도록 도와줍니다. |
| [DraggableRect](DraggableRect/README.md) | UI를 드래그 할 수 있게 만드는 컴포넌트입니다. |
| [ContentSizeSetter](ContentSizeSetter/README.md) | 다른 UI 콘텐츠 사이즈를 설정해 주는 컴포넌트입니다.|
| [WrapLayoutGroup](WrapLayoutGroup/README.md) | UI 사각영역(RectTansform) 내에서 수직, 또는 수평으로 자식 요소를 정렬시키는 컴포넌트입니다.|
| [WebCacheImage](WebCacheImage/README.md) | URL을 이용하여 웹 이미지를 캐싱 해서 보여주는 컴포넌트입니다.|
