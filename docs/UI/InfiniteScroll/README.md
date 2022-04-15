# Infinite Scroll

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [사용 방법](#사용-방법)
* [API](#-api)
* [Sample](#-sample)

## 개요

스크롤 사각 영역(Scroll Rect(Scroll View))을 사용할 때 뷰포트(Viewport) 크기에 맞게 아이템을 생성해 재사용할 수 있는 컴포넌트입니다.

* InfiniteScroll은 사용자가 삽입한 InfiniteScrollData(혹은 상속받은) 클래스로 콘텐츠(Content)의 요소(Element)를 생성합니다.
    * InfiniteScroll.InsertData()
* 콘텐츠의 요소로 사용할 프리팹(Prefab)에서는 InfiniteScrollItem(혹은 상속받은) 클래스를 연결해서 사용해야 합니다.
    * InfiniteScrollItem.UpdateData()에서 프리팹 로직 구현

## 사용 방법

### 생성
![inspector](images/inspector.png)
* 스크롤 사각 영역(Scroll Rect(Scroll View))이 붙어있는 오브젝트에 Infinite Scroll 컴포넌트를 추가합니다.
* Item Prefab에 InfiniteScrollItem을 상속받은 클래스가 붙어있는 프리팹을 추가합니다.

### 스크롤 데이타 적용
* InfiniteScrollItem 상속받은 클래스 내에서 콘텐츠(Content)의 데이타(Data)를 적용하여 사용합니다.
    ```
    public override void UpdateData(InfiniteScrollData scrollData)
    {
        base.UpdateData(scrollData);

        // InfiniteScrollData 콘텐츠로 데이타 적용
    }
    ```

### 아이템 동적 크기 조정
* Dynamic Item Size 옵션을 활성화합니다.
* InfiniteScrollItem 상속 받은 클래스
    * SetSize를 사용하여 크기를 변경합니다.
    * SetSize를 사용하지 않고 크기 변경 시 OnUpdateItemSize() 함수를 호출해 스크롤에 반영합니다.

### 스크롤 그리드 적용
* Layout의 Values 그리드를 분할할 크기를 설정합니다.
* Values의 Element의 비율로 그리드를 비율을 설정합니다.
    * ![grid_2](images/grid_2.png)
    * 아래와 같이 2:1:1 비율로 나눈 결과입니다.
    * 200, 100, 100등 1이 넘어간 값으로 크기에 맞춰서 지정할 수도 있습니다.
    * ![grid_1](images/grid_1.png)

### 스크롤 이벤트
ScrollView의 상태 변화에 따라 호출하는 이벤트 입니다.

Inspector나 AddListener를 통해 콜백 함수를 등록하여 활용할 수 있습니다.

#### 인스팩터
![event](images/event.png)

#### onChangeValue
ScrollView의 값이 변경되었을 때 호출하는 이벤트 입니다.
* (int)firstDataIndex
    * 스크롤에서 보이는 첫번째 Data의 Index
* (int)lastDataIndex
    * 스크롤에서 보이는 마지막 Data의 Index
* (bool)isStartLine
    * 스크롤이 시작 지점인지 여부
* (bool)isEndLine
    * 스크롤이 마지막 지점인지 여부
```cs
onChangeValue.AddListener(firstDataIndex, lastDataIndex, isStartLine, isEndLine =>
{
    // funtion
});
```

#### onChangeActiveItem
Scroll Item이 보이거나 사라질때 호출하는 이벤트 입니다.
* (int)dataIndex
    * 변경된 스크롤 Data의 Index
* (bool)active
    * 스크롤 아이템의 활성화 여부
```cs
onChangeActiveItem.AddListener(dataIndex, active =>
{
    // funtion
});
```

#### onStartLine
ScrollView의 시작 지점인지 여부가 바뀔때 호출하는 이벤트 입니다.
* (bool)isStartLine
    * 스크롤이 시작 지점인지 여부
```cs
onStartLine.AddListener((bool)isStartLine =>
{
    // funtion
});
```

#### onEndLine
ScrollView의 마지막 지점인지 여부가 바뀔때 호출하는 이벤트 입니다.
* (bool)isEndLine
    * 스크롤이 마지막 지점인지 여부
```cs
onEndLine.AddListener((bool)isEndLine =>
{
    // funtion
});
```


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

