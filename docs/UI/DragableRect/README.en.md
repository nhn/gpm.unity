# DragableRect

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#Overview)
* [How to use](#How-to-use)
* [Sample](#Sample)

## Overview

This component allows you to drag UI.

## How to use

Add **DragableRect** component to the UI object.

* Raycast Target must be enabled within the added UI in order for it to work.
* If you want to control the drag event only, add the **DragaEventHandler** component instead.

![DragableRect.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/DragableRect/images/DragableRect.png?raw=true)

1. You can add an event that will start upon mouse dragging.
2. You can add an event that will be triggered during mouse dragging.
3. You can add an event that will start at the end of the mouse dragging.
4. You can specify the UI you want to move by dragging. If None, it is automatically set to the UI containing the component.

## Sample

Assets/GPM/UI/Sample/DragableRect

![dragableRectSample.gif](https://github.com/nhn/gpm.unity/blob/main/docs/UI/DragableRect/images/dragableRectSample.gif?raw=true)