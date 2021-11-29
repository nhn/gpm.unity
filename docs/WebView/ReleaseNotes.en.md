# Release notes

🌏 [한국어](ReleaseNotes.md)

## 1.3.2

### Date

* 2021.11.29

### Fixed
#### iOS

* Fixed a bug that caused the previous page to reload when trying to navigate to a linked page on certain webpages.

### Improved

* Add warning log when calling the WebView API that does not work in Unity Editor.

---

## 1.3.1

### Date

* 2021.08.12

### Fixed

* Disable Lumin in the Exclude Platforms attribute of assembly definitions.
* Add the default value for Configuration.navigationBarColor

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
