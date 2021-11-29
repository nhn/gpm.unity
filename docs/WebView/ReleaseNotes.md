# Release notes

🌏 [English](ReleaseNotes.en.md)

## 1.3.2

### Date

* 2021.11.29

### Fixed
#### iOS
* 일부 웹페이지에서 링크된 페이지로 이동하려고 할 때 이전의 페이지가 다시 로드되는 문제 수정

### Improved

* Unity Editor에서 동작하지 않는 WebView API를 호출하면 warning log가 발생하도록 수정

---

## 1.3.1

### Date

* 2021.08.12

### Fixed

* Assembly definitions의 Exclude Platforms 속성에서 Lumin을 비활성화
* Configuration.navigationBarColor의 기본 값 추가

---

## 1.3.0

### Date

* 2021.07.31

### Added

* Configuration
    * navigationBarColor
    * supportMultipleWindows (Android only)
* Assembly definition

---

## 1.2.0

### Date

* 2021.03.12

### Added

* Configuration
    * isNavigationBarVisible
    * isClearCookie
    * isClearCache

---

## 1.1.0

### Date

* 2021.02.23

### Added

* Configuration
    * Popup Style
    * Forward Button
* API
    * ShowHtmlFile
    * ShowHtmlString
    * ExecuteJavaScript

### Removed

* Configuration
    * Orientation

---

## 1.0.0

### Date

* 2020.12.24

### Features

* Platform 
    * Android
    * iOS

* API
    * ShowUrl
    * Close
