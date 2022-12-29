# ContentSizeSetter

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#Overview)
* [How to use](#How-to-use)
* [Sample](#Sample)

## Overview

This component sets the size of other UI content.

## How to use
Add the **ContentSizeSetter** component to the UI object that will be the reference.
Add the target to change the size to the target.

![ContentSizeSetter.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/ContentSizeSetter/images/ContentSizeSetter.png?raw=true)
1. You can add an event that will start upon mouse dragging.
2. Set the target to change the size.

## Sample

Assets/GPM/UI/Sample/CotentSizeSetter

![CotentSizeSetterSample.gif](https://github.com/nhn/gpm.unity/blob/main/docs/UI/ContentSizeSetter/images/CotentSizeSetterSample.gif?raw=true)

In this sample, **ContentSizeSetter** is being used in the following circumstances:
1. To set ContentsSizeFrame larger than EntryRoot size by (5, 5)
2. To set TextBox larger than Text__Value by (10, 8) in the entity prefab
3. To set ChildContainer larger than ChildRoot by (10, 0)

In this sample, LayoutGroup and ContentSizeFitter are nested and used at the same time.
In this case, the size and layout might not be updated properly depending on the action sequence, 
so use the **LayoutUpdater** component instead to update the parents layout.
**LayoutUpdater** passes the layout update information to the parent object.