# Release notes

🌏 [한국어](ReleaseNotes.md)

## 1.8.0

### Date
* 2022.08.04

### Added
* Android WebChromeClient permissions

## 1.7.1

### Date
* 2022.07.08

### Updated
* Updated Common 2.0.4 to 2.1.2
* Updated Communicator 1.0.2 to 1.1.0

## 1.7.0

### Date

* 2022.05.27

### Added

* Supports SafeBrowsing
  * Android Chrome CustomTabsIntent
  * iOS SFSafariViewController

* Added WebView Show API callback
  * Deprecated each callback
  * WebView event processing based on CallbackType

* Added auto rotation
  * WebView configuration variable : isAutoRotation
  * iOS only
  * Specifies true only when Screen.orientation is not set manually.

### Updated

* Deprecated API

```cs
[System.Obsolete("This method is deprecated.")]
public static void ShowUrl(
    string url,
    GpmWebViewRequest.Configuration configuration,
    GpmWebViewCallback.GpmWebViewErrorDelegate openCallback,
    GpmWebViewCallback.GpmWebViewErrorDelegate closeCallback,
    List<string> schemeList,
    GpmWebViewCallback.GpmWebViewDelegate<string> schemeEvent)

[System.Obsolete("This method is deprecated.")]
public static void ShowUrl(
    string url,
    GpmWebViewRequest.Configuration configuration,
    GpmWebViewCallback.GpmWebViewErrorDelegate openCallback = null,
    GpmWebViewCallback.GpmWebViewErrorDelegate closeCallback = null,
    GpmWebViewCallback.GpmWebViewPageLoadDelegate pageLoadCallback = null,
    List<string> schemeList = null,
    GpmWebViewCallback.GpmWebViewDelegate<string> schemeEvent = null)

[System.Obsolete("This method is deprecated.")]
public static void ShowHtmlFile(
    string filePath,
    GpmWebViewRequest.Configuration configuration,
    GpmWebViewCallback.GpmWebViewErrorDelegate openCallback,
    GpmWebViewCallback.GpmWebViewErrorDelegate closeCallback,
    List<string> schemeList,
    GpmWebViewCallback.GpmWebViewDelegate<string> schemeEvent)

[System.Obsolete("This method is deprecated.")]
public static void ShowHtmlFile(
    string filePath,
    GpmWebViewRequest.Configuration configuration,
    GpmWebViewCallback.GpmWebViewErrorDelegate openCallback = null,
    GpmWebViewCallback.GpmWebViewErrorDelegate closeCallback = null,
    GpmWebViewCallback.GpmWebViewPageLoadDelegate pageLoadCallback = null,
    List<string> schemeList = null,
    GpmWebViewCallback.GpmWebViewDelegate<string> schemeEvent = null)

[System.Obsolete("This method is deprecated.")]
public static void ShowHtmlString(
    string htmlString,
    GpmWebViewRequest.Configuration configuration,
    GpmWebViewCallback.GpmWebViewErrorDelegate openCallback = null,
    GpmWebViewCallback.GpmWebViewErrorDelegate closeCallback = null,
    List<string> schemeList = null,
    GpmWebViewCallback.GpmWebViewDelegate<string> schemeEvent = null,
    GpmWebViewCallback.GpmWebViewPageLoadDelegate pageLoadCallback = null)
```

## 1.6.0

### Date

* 2022.05.16

### Added

* Supports file upload
  * Android API 21 or later

* Added custom user agent string
  * WebView configuration variable : userAgentString
  
* Supports multiple windows (new window on the WebView)
  * WebView configuration variable : supportMultipleWindows

* Added WebView API
  * getX
  * getY
  * getWidth
  * getHeight

## 1.5.1

### Date

* 2022.05.11

### Fixed

* iOS WebView custom scheme callback

## 1.5.0

### Date

* 2022.04.20

### Updated

* WebView configuration
  * isNavigationBarVisible
    * Activate/Deactivate close button of iOS Popup WebView.

* Sample.scene, SampleWebView.cs
  * How to use Popup WebView as APIs and configurations.

### Added

* Added WebView API
  * SetPosition
  * SetSize
  * SetMargins
  * IsActive

* Added WebView configuration variables
  * position
  * size
  * margins
  * isMaskViewVisible
    * Activate/Deactivate background mask view of Popup WebView (iOS only)

## 1.4.1

### Date

* 2022.03.11

### Fixed

* Fixed inconsistent line endings in SampleWebView.cs file.

#### iOS

* Fixed URL with Korean characters encoding error. ([#186](https://github.com/nhn/gpm.unity/issues/186))

## 1.4.0

### Date

* 2022.03.04

### Added

* Added WebView API
  * CanGoBack
  * CanGoForward
  * GoBack
  * GoForward
* Added WebView Sample scene ([#105](https://github.com/nhn/gpm.unity/issues/105))

### Updated

* Modify WebView API
  * Added OnPageLoadCallback parameter to ShowUrl, ShowHtmlFile, ShowHtmlString ([#71](https://github.com/nhn/gpm.unity/issues/71))

---

## 1.3.2

### Date

* 2021.11.29

### Fixed
#### iOS

* Fixed a bug that caused the previous page to reload when trying to navigate to a linked page on certain webpages.

### Updated

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

### Updated

* Configuration
    * Orientation removed

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
