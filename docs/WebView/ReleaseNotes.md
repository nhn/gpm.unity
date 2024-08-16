# Release notes

🌏 [English](ReleaseNotes.en.md)

## 2.1.0

### Date

* 2024.08.16

### Added

* (iOS) CloseSafeBrowsing API 추가 [(396)](https://github.com/nhn/gpm.unity/issues/396) [(522)](https://github.com/nhn/gpm.unity/issues/522)
* (iOS) 페이지 로딩이 느리면 닫기 버튼이 없어서 페이지를 닫지 못하는 이슈 개선 [(434)](https://github.com/nhn/gpm.unity/issues/434)

### Fixed

* (Android) ShowSafeBrowsing API: 디바이스에 설정된 기본 브라우저로 열리는 이슈 개선 [(520)](https://github.com/nhn/gpm.unity/issues/520)
* (Android) 오류 코드가 string으로 전달되어, Unity에서 Json 파싱 오류가 발생하는 이슈 수정 [(454)](https://github.com/nhn/gpm.unity/issues/454)
* 내부 로직 개선

## 2.0.5

### Date

* 2024.04.29

### Fixed
* (Android) HTML 문자열에 #이 포함되면 오류가 발생하는 이슈 개선 [(473)](https://github.com/nhn/gpm.unity/issues/473)

## 2.0.4

### Date

* 2024.04.03

### Fixed
* 'Undefined symbols for architecture arm64' 오류 수정 [(501)](https://github.com/nhn/gpm.unity/issues/501)

## 2.0.3

### Date

* 2024.03.29

### Updated
* Apple 개인정보 보호 정책 대응 [(Apple Privacy Policy)](https://developer.apple.com/news/?id=3d8a9yyh)

## 2.0.2

### Date
* 2023.10.17

### Fixed
* iOS close button 활성/비활성 설정 수정([Issue 450](https://github.com/nhn/gpm.unity/issues/450))

## 2.0.1

### Date
* 2023.10.10

### Fixed
* Android screen position, size layout 계산 오류 수정([Issue 445](https://github.com/nhn/gpm.unity/issues/445), [Issue 446](https://github.com/nhn/gpm.unity/issues/446))

## 2.0.0

### Date
* 2023.09.22

### Added
* Android back button으로 WebView가 닫힐 때 callback으로 대체(Android only) ([Issue 422](https://github.com/nhn/gpm.unity/issues/422))
  * GpmWebViewRequest.Configuration isBackButtonCloseCallbackUsed
  * GpmWebViewCallback.CallbackType.BackButtonClose
* Close button 활성/비활성 설정 추가([Issue 423](https://github.com/nhn/gpm.unity/issues/423))
  * GpmWebViewRequest.Configuration isCloseButtonVisible

### Updated
* Popup WebView의 설정 영역만 차지하도록 변경([Issue 421](https://github.com/nhn/gpm.unity/issues/421), [Issue 416](https://github.com/nhn/gpm.unity/issues/416), [Issue 351](https://github.com/nhn/gpm.unity/issues/351), [Issue 280](https://github.com/nhn/gpm.unity/issues/280))

### Fixed
* Deprecated API 제거(ShowUrl, ShowHtmlFile, ShowHtmlString)
* ScreenOrientation.Landscape를 LandscapeLeft로 변경

## 1.12.2

### Date
* 2023.08.23

### Fixed
* GpmWebView class의 deprecated APIs 위치 변경

## 1.12.1

### Date
* 2023.06.20

### Fixed
* Android WebView에서 정의되지 않은 scheme 오류 수정([Issue407](https://github.com/nhn/gpm.unity/issues/407), [Issue 410](https://github.com/nhn/gpm.unity/issues/410))

## 1.12.0

### Date
* 2023.06.19

### Added
* GpmWebViewCallback.CallbackType.PageStarted 콜백 추가([Issue 354](https://github.com/nhn/gpm.unity/issues/354))
* GpmWebViewRequest.Configuration에 WebView 배경 색상 추가([Issue 354](https://github.com/nhn/gpm.unity/issues/354))

## 1.11.1

### Date
* 2023.01.30

### Fixed
* GpmWebViewRequest.Configuration의 NullReferenceException 오류 수정([Issue 348](https://github.com/nhn/gpm.unity/issues/348))

## 1.11.0

### Date
* 2023.01.12

### Added
* Custom scheme 후처리 명령 추가([Issue 328](https://github.com/nhn/gpm.unity/issues/328))
  * 명령 : Close, LoadUrl, ExecuteJavascript

## 1.10.0

### Date
* 2022.12.09

### Added
* ExecuteJavascript 결과 콜백 추가 ([Issue 296](https://github.com/nhn/gpm.unity/issues/296))
* JavaScript Injection 기능 추가 ([Discussion 297](https://github.com/nhn/gpm.unity/discussions/297))
  * GpmWebViewRequest.Configuration.addJavascript

### Fixed
* Android custom scheme을 지정한 값으로 저장되게 수정 ([Issue 288](https://github.com/nhn/gpm.unity/issues/288))
* iOS 전체 화면이 일부 잘리는 현상 수정 ([Issue 313](https://github.com/nhn/gpm.unity/issues/313))

## 1.9.2

### Date
* 2022.11.02

### Updated
* iOS WebView 스킴 목록 중 "itms-servies"가 앱 스토어 심사에서 거절되는 경우가 발생하여 제거

## 1.9.1

### Date
* 2022.10.13

### Updated
* Android WebViewClient 클래스의 shouldOverrideUrlLoading 로직 개선
  * URL에 대한 scheme key 수정("intent://" -> "intent:")
  * "intent:", "market://" 이외의 scheme을 ACTION_VIEW로 처리

## 1.9.0

### Date
* 2022.09.20

### Added
* 화면 회전 지원을 위한 옵션 추가
* 디바이스 기본 브라우저 호출 API
* 파일 다운로드 기능 (Android only)

### Updated
* Unity Guidelines의 1.3.a Versions of Unity 내용에 따라 최소 버전을 2019.4로 상향
  * 참조 : [Unity Guidelines](https://assetstore.unity.com/publishing/submission-guidelines)

## 1.8.1

### Date
* 2022.08.09

### Updated
* iOS redirect scheme 업데이트

## 1.8.0

### Date
* 2022.08.04

### Added
* Android WebChromeClient 권한 허용 기능 추가

## 1.7.1

### Date
* 2022.07.08

### Updated
* Common 2.0.4를 2.1.2로 업데이트
* Communicator 1.0.2를 1.1.0으로 업데이트

## 1.7.0

### Date

* 2022.05.27

### Added

* SafeBrowsing 지원
  * Android Chrome CustomTabsIntent
  * iOS SFSafariViewController

* WebView Show API callback 수정
  * 개별 callback 지원 deprecated
  * CallbackType에 따라 WebView 이벤트 처리

* auto rotation 변수 추가
  * WebView configuration 변수 : isAutoRotation
  * iOS only
  * Screen.orientation을 수동 설정하지 않을 때만 true로 지정

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

* File upload 지원
  * Android API 21 이상

* Custom user agent string 추가
  * WebView configuration 변수 : userAgentString

* Multiple windows 지원 (WebView의 새창 지원)
  * WebView configuration 변수 : supportMultipleWindows

* WebView API 추가
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
    * iOS Popup WebView close button 활성화/비활성화

* Sample.scene, SampleWebView.cs
  * API와 configuration으로 Popup WebView를 사용하는 방법

### Added

* WebView API 추가
  * SetPosition
  * SetSize
  * SetMargins
  * IsActive

* WebView configuration 변수 추가
  * position
  * size
  * margins
  * isMaskViewVisible
    * Popup WebView 배경 mask view 활성화/비활성화 (iOS only)

## 1.4.1

### Date

* 2022.03.11

### Fixed

* SamepleWebView.cs 파일의 일관성 없는 line ending 수정

#### iOS

* 한글이 포함된 URL 인코딩 오류 수정 ([#186](https://github.com/nhn/gpm.unity/issues/186))

## 1.4.0

### Date

* 2022.03.04

### Added

* WebView API 추가
  * CanGoBack
  * CanGoForward
  * GoBack
  * GoForward
* WebView Sample scene 추가 ([#105](https://github.com/nhn/gpm.unity/issues/105))

### Updated

* WebView API 수정
  * ShowUrl, ShowHtmlFile, ShowHtmlString에 OnPageLoadCallback 매개변수 추가 ([#71](https://github.com/nhn/gpm.unity/issues/71))

---

## 1.3.2

### Date

* 2021.11.29

### Fixed
#### iOS
* 일부 웹페이지에서 링크된 페이지로 이동하려고 할 때 이전의 페이지가 다시 로드되는 문제 수정

### Updated

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

### Updated

* Configuration
    * Orientation 제거

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
