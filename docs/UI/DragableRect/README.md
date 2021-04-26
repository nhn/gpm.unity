# DragableRect

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [사용 방법](#사용-방법)
* [Sample](#Sample)

## 개요

UI를 드래그 할수 있게 만드는 컴포넌트입니다.

## 사용 방법
UI 오브젝트에 **DragableRect** 컴포넌트를 추가합니다.
* 추가된 UI내에 Raycast Target이 활성화되어야 동작합니다.
* 드래그 이벤트만 제어하고 싶다면 **DragaEventHandler** 컴포넌트를 대신 추가할수 있습니다.

![DragableRect.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/DragableRect/images/DragableRect.png?raw=true)

1. 드레그가 시작될때의 이벤트를 추가할수 있습니다.
2. 드레그가 중일때의 이벤트를 추가할수 있습니다.
3. 드레그가 종료될때의 이벤트를 추가할수 있습니다.
4. 드래그로 움직일 UI를 지정할수 있습니다. None일경우 컴포넌트를 넣은 UI로 자동으로 설정됩니다.


## Sample

Assets/GPM/UI/Sample/DragableRect

![dragableRectSample.gif](https://github.com/nhn/gpm.unity/blob/main/docs/UI/DragableRect/images/dragableRectSample.gif?raw=true)
