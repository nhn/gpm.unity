# Release notes

🌏 [한국어](ReleaseNotes.md)

## 2.10.0

### Date

* 2024.09.25

### Added
* WebCacheImage
    * Function to add headers
    * Function to select cache request types
    * Function to change cache re-request time
    * Function to set minimum and maximum validity for cache

## 2.9.0

### Date

* 2024.3.8

### Added

* InfiniteScroll
    * Introduced functionality to modify the reference point and direction([438](https://github.com/nhn/gpm.unity/issues/438), [455](https://github.com/nhn/gpm.unity/issues/455))
        * ![infinitescroll_item](InfiniteScroll/images/infinitescroll_item.gif)
    * Implemented a data filtering feature([442](https://github.com/nhn/gpm.unity/issues/442))
        * ![infinitescroll_filter](InfiniteScroll/images/infinitescroll_filter.gif)

### Updated

* InfiniteScroll
    * Improved functionality to apply space and padding alignment along the axis (x, y)
        * ![infinitescroll_space_padding](InfiniteScroll/images/infinitescroll_space_padding.gif)

### Fixed
* InfiniteScroll
    * Fixed an issue where object management was not handled properly when data was added in the middle([470](https://github.com/nhn/gpm.unity/issues/470)) 

## 2.8.0

### Date

* 2023.11.24

### Added
* InfiniteScroll
    * Added InsertData API to add data to a specified location([438](https://github.com/nhn/gpm.unity/issues/438))

### Fixed
* InfiniteScroll
    * Fixed so that updates are not affected according to the component update order after active([413](https://github.com/nhn/gpm.unity/issues/413))
* MultiLayout
    * Fixed position change issue according to pivot([456](https://github.com/nhn/gpm.unity/issues/456))

### Updated
* InfiniteScroll
    * Position typo correction

## 2.7.3

### Date

* 2023.6.1

### Fixed
* TabController
   * Fixed a bug where changes were not being applied in the prefab stage.
   * Fixed a bug where links were being removed when saving prefabs in certain Unity versions.

### Updated
* Updated Common 2.3.1.
* Updated CacheStorage 1.3.0.
* WebCacheImage
   * Improved to cancel previous requests when the URL is changed.
* TabController
   * Improved to not automatically remove empty items.


## 2.7.2

### Date

* 2023.4.24

### Updated
* Updated Common 2.3.0
* Updated CacheStorage 1.2.0

## 2.7.1

### Date

* 2023.2.21

### Fixed
* InfiniteScroll
    * Fixed a problem where the UpdateData function was called many times unnecessarily([355](https://github.com/nhn/gpm.unity/issues/355))
    
    * Fixed so that it works normally when Move is called immediately after calling InsertData([356](https://github.com/nhn/gpm.unity/issues/355))
    
### Updated
* InfiniteScroll
    * Improved to update Item when calling UpdateData function

## 2.7.0

### Date

* 2022.12.23

### Added
* Added TabControl
    * The TabControl component controls Tabs and TabPages that are frequently used in the UI.
    * [TabControl Guide](TabControl/README.en.md)

![preview](images/tabcontrol_preview.gif)
    
### Fixed
* InfiniteScroll
    * Fixed an issue where the scroll size was calculated incorrectly depending on the point in time when changing the item size in the CanvasUpdate logic
    * Fixed an issue where a warning occurred when creating TextMeshPro in CanvasUpdate logic

### Updated
* InfiniteScroll
    * change to delay update
    * Optimized to create and reuse fewer scroll items

## 2.6.0

### Date

* 2022.11.02

### Added
* InfiniteScroll
    * Added smooth scroll movement
* ResizeLayoutHandler
    * Added a module that lets you know events when they are resized

## 2.5.1

### Date

* 2022.07.08

### Updated

* Updated Common 2.1.0 to 2.1.2

## 2.5.0

### Date

* 2022.05.30

### Added
* Added WebCacheImage

### Updated
* Added Common v2.1.0 dependency
* Added CacheStorage v0.1.0 dependency

### Fixed
* InfiniteScroll
    * Fixed the problem that scroll items are not reused after clearing the list

## 2.4.0

### Date

* 2022.04.18

### Added
* InfiniteScroll
    * Added Scroll Event [(180)](https://github.com/nhn/gpm.unity/issues/180)
        * OnChangeValue
        * OnChangeActiveItem
        * OnStartLine
        * OnEndLine

* WrapLayoutGroup
    * Added Samples
    * Added a document

## 2.3.0

### Date

* 2022.03.21

### Added
* InfiniteScroll
    * Added a function to split into a Grid [(161)](https://github.com/nhn/gpm.unity/issues/161)

### Fixed
* InfiniteScroll
    * Fixed the problem that the list is not displayed according to the initialization order

## 2.2.0

### Date

* 2022.02.21

### Added
* Added WrapLayoutGroup

## 2.1.1

### Date

* 2022.01.17

### Fixed
* InfiniteScroll
    * Fixed a problem where ScrollItem Item size was incorrectly calculated as total size 0

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