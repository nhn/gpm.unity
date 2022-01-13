# Release notes

🌏 [한국어](ReleaseNotes.md)


🌏 [English](ReleaseNotes.en.md)

## 2.1.0

### Date

* 2022.01.13

### Added
* InfiniteScroll
    * Added ScrollItem active function
    * Added ScrollItem Item size setting function

### Updated
* InfiniteScroll
    * Update to be able to respond to variable-length ScrollItems in dynamicItemSize environment [(165)](https://github.com/nhn/gpm.unity/issues/165)

### Fixed
* InfiniteScroll
    * Fixed an issue where invisible ScrollItem object was activated in dynamicItemSize environment

## 2.0.7

### Date

* 2020.06.21

### Added
* InfiniteScroll
    * Added scroll item spacing function

## 2.0.6

### Date

* 2020.05.26

### Fixed
* InfiniteScroll
    * Correction of error when calling Clear before initialization

## 2.0.5

### Date

* 2020.05.13

### Changed
* DragableRect renamed to DraggableRect

## 2.0.4

### Date

* 2020.05.03

### Updated
* ContentSizeSetter
    * ExecuteInEditMode changed to ExcuteAlways as a popup issue in prefab mode
* LayoutUpdate
    * ExecuteInEditMode changed to ExcuteAlways as a popup issue in prefab mode

### Fixed
* DragableRect 
    * Fixed a problem where events are accumulated when repeating on/off
* LayoutUpdate
    * Added exception handling when parent RectTransform does not exist.

## 2.0.3

### Date

* 2020.04.16

### Added
* Add DrawableRect feature
* Add ContentSizeFitter  feature

### Updated
* Improvement InfiniteScroll initialization logic 
* Change folder structure 

## 2.0.2

### Date

* 2020.03.11

### Fixed

* Fix comfile error when building after applying Asseambly Definition

## 2.0.1

### Date

* 2020.03.10

### Added

* Add Assembly Definition

## 2.0.0

### Date

* 2020.12.21

### Updated

* Brand name changed to Game Package Manager from TOAST Kit.

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