# Infinite Scroll

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [API](#-api)
* [Sample](#-sample)

## 개요

스크롤 사각 영역(Scroll Rect(Scroll View))을 사용할 때 뷰포트(Viewport) 크기에 맞게 아이템을 생성해 재사용할 수 있는 컴포넌트입니다.

* InfiniteScroll은 사용자가 삽입한 InfiniteScrollData(혹은 상속받은) 클래스로 콘텐츠(Content)의 요소(Element)를 생성합니다.
    * InfiniteScroll.InsertData()
* 콘텐츠의 요소로 사용할 프리팹(Prefab)에서는 InfiniteScrollItem(혹은 상속받은) 클래스를 연결해서 사용해야 합니다.
    * InfiniteScrollItem.UpdateData()에서 프리팹 로직 구현

## 🔨 API

API 사용 방법은 Assets/GPM/UI/Sample/InfiniteScroll/Scripts/InfiniteScrollSample.cs를 참고하시기 바랍니다.

### InsertData

콘텐츠의 요소로 보여줄 데이터를 추가합니다.

```cs
public void InsertData(InfiniteScrollData data)
```

### UpdateData

삽입한 데이터를 업데이트합니다.

```cs
public void UpdateData(InfiniteScrollData data)
```

### UpdateAllData

모든 데이터를 업데이트합니다.

```cs
public void UpdateAllData()
```

### RemoveData

삽입한 데이터를 삭제합니다.

```cs
public void RemoveData(InfiniteScrollData data)
```
```cs
public void RemoveData(int dataIndex)
```

### Clear

모든 데이터를 삭제합니다.

```cs
public void Clear()
```

### MoveToFirstData

첫 번째 데이터로 콘텐츠를 이동합니다.

```cs
public void MoveToFirstData()
```

### MoveToLastData

마지막 데이터로 콘텐츠를 이동합니다.

```cs
public void MoveToLastData()
```

### IsMoveToLastData

콘텐츠가 마지막 데이터로 이동했는지 확인합니다.

```cs
public bool IsMoveToLastData()
```

### MoveTo

해당 데이터로 콘텐츠를 이동합니다.

```cs
public void MoveTo(InfiniteScrollData data, MoveToType moveToType)
```

```cs
public void MoveTo(int dataIndex, MoveToType moveToType)
```

### ResizeScrollView

ScrollView 크기가 변경되었을 때 Infinite Scroll에서 크기 변경을 처리하는 데 필요한 API입니다.

```cs
public void ResizeScrollView()
```

## 🐾 Sample

Assets/GPM/UI/Sample/InfiniteScroll

![infinitescroll_sample](images/infinitescroll_sample.gif)

---

![dynamic_sample](images/dynamic_sample.gif)

