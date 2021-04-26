# ContentSizeSetter

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [사용 방법](#사용-방법)
* [Sample](#-sample)

## 개요

다른 UI컨텐츠 사이즈를 설정해주는 컴포넌트입니다.

## 사용 방법
기준이될 UI 오브젝트에 **ContentSizeSetter** 컴포넌트를 추가합니다.
사이즈를 변경할 대상을 Target에 추가합니다..

![ContentSizeSetter.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/ContentSizeSetter/images/ContentSizeSetter.png?raw=true)
1. 드레그가 시작될때의 이벤트를 추가할수 있습니다.
2. 사이즈를 변경할 대상을 설정합니다.

## Sample

Assets/GPM/UI/Sample/CotentSizeSetter

![CotentSizeSetterSample.gif](https://github.com/nhn/gpm.unity/blob/main/docs/UI/ContentSizeSetter/images/CotentSizeSetterSample.gif?raw=true)

해당 셈플에서는 **ContentSizeSetter**를 아래와 같은 상황에 사용하고 있습니다.
1. ContentsSizeFrame가 EntryRoot 크기 보다 (5, 5) 더 큰 크기로 설정
2. Entity 프리팹에서 TextBox가 Text_Value 크기 보다 (10, 8) 더 큰 크기로 설정
3. ChildContainer가 ChildRoot 크기 보다 (10, 0) 더 큰 크기로 설정

해당 셈플에서는 LayoutGroup와 ContentSizeFitter를 중첩하여 사용하고 있습니다.
이럴경우 동작 순서에 의해 크기나 레이아웃이 갱신이 제대로 되지 않기 때문에 
**LayoutUpdater**을 컴포넌트를 이용해 부모 레이아웃을 갱신해줍니다.
**LayoutUpdater**는 부모 오브젝트에 레이아웃 갱신정보를 전달해줍니다.