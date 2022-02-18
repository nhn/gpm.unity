# Release notes

🌏 [English](ReleaseNotes.en.md)

## 2.2.0

### Date

* 2022.02.21

### Added
* WrapLayoutGroup 추가

## 2.1.1

### Date

* 2022.01.17

### Fixed
* InfiniteScroll
    * ScrollItem Item size 전체 사이즈 0으로 잘못 계산하는 문제 수정

## 2.1.0

### Date

* 2022.01.13

### Added
* InfiniteScroll
    * ScrollItem active 함수 추가
    * ScrollItem Item size 설정 함수 추가

### Updated
* InfiniteScroll
    * dynamicItemSize 환경에서 가변길이 ScrollItem 대응 가능하도록 수정 로직 수정[(165)](https://github.com/nhn/gpm.unity/issues/165)

### Fixed
* InfiniteScroll
    * dynamicItemSize 환경에서 보이지 않는 ScrollItem 오브젝트 활성화 되는 문제 수정

## 2.0.7

### Date

* 2020.06.21

### Added
* InfiniteScroll
    * 스크롤 아이템 간격 기능 추가

## 2.0.6

### Date

* 2020.05.26

### Fixed
* InfiniteScroll
    * 초기화 전 Clear 호출할 때 오류 수정

## 2.0.5

### Date

* 2020.05.13

### Changed
* DragableRect DraggableRect로 이름 변경

## 2.0.4

### Date

* 2020.05.03

### Updated
* ContentSizeSetter
    * ExecuteInEditMode 프리팹 모드 팝업 이슈로 ExcuteAlways로 변경
* LayoutUpdate
    * ExecuteInEditMode 프리팹 모드 팝업 이슈로 ExcuteAlways로 변경

### Fixed
* DragableRect 
    * 온/오프 반복 시 이벤트 누적되는 문제 수정
* LayoutUpdate
    * 부모 RectTransform가 없을 경우에 대한 예외 처리를 추가합니다.

## 2.0.3

### Date

* 2020.04.16

### Added
* DragableRect 기능 추가
* ContentSizeSetter 기능 추가

### Updated
* InfiniteScroll 초기화 로직 개선
* 폴더 구조 변경

## 2.0.2

### Date

* 2020.03.11

### Fixed

* Asseambly Definition 적용 후 빌드시 컴파일 오류 수정

## 2.0.1

### Date

* 2020.03.10

### Added

* Assembly Definition 적용

### 2.0.0

### Date

* 2020.12.21

### Updated

* TOAST Kit에서 Game Package Manager로 브랜드 이름 변경

---

## 1.1.0

### Added

#### Infinite Scroll

* Support dynamic item size

## 1.0.1

### Fixed

#### Infinite Scroll

* Fixed initialization problem related to Item in Clear().

## 1.0.0

### Features

* MultiLayout
* InfiniteScroll