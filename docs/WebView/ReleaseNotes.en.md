# Release notes

🌏 [한국어](ReleaseNotes.md)

## 2.0.5

### Date

* 2024.04.26

### Fixed
* (Android) Improves an issue where an error occurs when an HTML string contains # [(473)](https://github.com/nhn/gpm.unity/issues/473)

## 2.0.4

### Date

* 2024.04.03

### Fixed
* Fixed 'Undefined symbols for architecture arm64' error [(501)](https://github.com/nhn/gpm.unity/issues/501)

## 2.0.3

### Date

* 2024.03.29

### Updated
* Response to Apple Privacy Policy [(Apple Privacy Policy)](https://developer.apple.com/news/?id=3d8a9yyh)

## 2.0.2

### Date
* 2023.10.17

### Fixed
* Fix iOS close button visible setting([Issue 450](https://github.com/nhn/gpm.unity/issues/450))

## 2.0.1

### Date
* 2023.10.10

### Fixed
* Fixed Android screen position, size layout calculation error([Issue 445](https://github.com/nhn/gpm.unity/issues/445), [Issue 446](https://github.com/nhn/gpm.unity/issues/446))

## 2.0.0

### Date
* 2023.09.22

### Added
* Use the back button to pass a callback instead of closing a WebView(Android only) ([Issue 422](https://github.com/nhn/gpm.unity/issues/422))
  * GpmWebViewRequest.Configuration isBackButtonCloseCallbackUsed
  * GpmWebViewCallback.CallbackType.BackButtonClose
* Add an option to set the visibility of the Close button([Issue 423](https://github.com/nhn/gpm.unity/issues/423))
  * GpmWebViewRequest.Configuration isCloseButtonVisible

### Updated
* Set the WebView to occupy only the size of the popup area([Issue 421](https://github.com/nhn/gpm.unity/issues/421), [Issue 416](https://github.com/nhn/gpm.unity/issues/416), [Issue 351](https://github.com/nhn/gpm.unity/issues/351), [Issue 280](https://github.com/nhn/gpm.unity/issues/280))

### Fixed
* Remove deprecated APIs(ShowUrl, ShowHtmlFile, ShowHtmlString)
* Change ScreenOrientation.Landscape to LandscapeLeft

## 1.12.2

### Date
* 2023.08.23

### Fixed
* Relocate deprecated APIs in GpmWebView class

## 1.12.1

### Date
* 2023.06.20

### Fixed
* Fixed the unknown custom scheme error in Android WebView([Issue407](https://github.com/nhn/gpm.unity/issues/407), [Issue 410](https://github.com/nhn/gpm.unity/issues/410))

## 1.12.0

### Date
* 2023.06.19

### Added
* Add GpmWebViewCallback.CallbackType.PageStarted callback([Issue 354](https://github.com/nhn/gpm.unity/issues/354))
* Add WebView background color to GpmWebViewRequest.Configuration([Issue 354](https://github.com/nhn/gpm.unity/issues/354))

## 1.11.1

### Date
* 2023.01.30

### Fixed
* Fixed NullReferenceException of GpmWebViewRequest.Configuration([Issue 348](https://github.com/nhn/gpm.unity/issues/348))

## 1.11.0

### Date
* 2023.01.12

### Added
* Add Custom scheme postprocessing command([Issue 328](https://github.com/nhn/gpm.unity/issues/328))
  * Command : Close, LoadUrl, ExecuteJavascript

## 1.10.0

### Date
* 2022.12.09

### Added
* Added ExecuteJavascript result callback ([Issue 296](https://github.com/nhn/gpm.unity/issues/296))
* Added JavaScript Injection feature ([Discussion 297](https://github.com/nhn/gpm.unity/discussions/297))
  * GpmWebViewRequest.Configuration.addJavascript

### Fixed
* Fixed Android custom scheme to save to specified value ([Issue 288](https://github.com/nhn/gpm.unity/issues/288))
* Fixed partial cropped issue of the full screen ([Issue 313](https://github.com/nhn/gpm.unity/issues/313))

## 1.9.2

### Date
* 2022.11.02

### Updated
* Removed "itms-services" out of the scheme list used in iOS WebView because it was rejected by App Review.

## 1.9.1

### Date
* 2022.10.13

### Updated
* Improved the shouldOverrideUrlLoading logic of the Android WebViewClient class
  * Modified scheme key for URL("intent://" -> "intent:")
  * Proceed to ACTION_VIEW except for "intent:", "market://"

## 1.9.0

### Date
* 2022.09.20

### Added
* Added options for screen rotation support
* Device default browser call API
* File download function (Android only)

### Updated
* Raise the minimum version to 2019.4 according to the 1.3.a Versions of Unity contents of the Unity Guidelines.
  * Link : [Unity Guidelines](https://assetstore.unity.com/publishing/submission-guidelines)

## 1.8.1

### Date
* 2022.08.09

### Updated
* Updated iOS redirect scheme

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
