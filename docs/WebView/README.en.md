# WebView

🌏 [한국어](README.md)

## 🚩 목차

* [개요](#개요)
* [스펙](#스펙)
* [플랫폼별 설정](#-플랫폼별-설정)
* [API](#-api)


## 개요
게임에서 다양하게 사용할 수 있는 웹뷰를 제공합니다.

## 스펙

### Unity 지원 버전

* 2018.4.0 이상

### Android 지원 버전

* 4.4 이상

### iOS 지원버전

* 11 이상

### 지원 플랫폼

* Anroid
* iOS 

### 지원하는 기능
| Category | Spec |
| --- | --- |
| Navigation | title |
|  | back |
|  | close |
| ShowUrl API | url |
|  | open Callback |
|  | close Callback |
|  | scheme Callback |
|  | schemeList |

## 🔨 플랫폼별 설정

###  Android

WebView는 [Gradle](https://docs.unity3d.com/Manual/android-gradle-overview.html)을 사용하여 Android에서 필요한 종속성을 설정합니다.
Unity 2019.3 이전 버전에 프로젝트에서는 **Internal** 빌드 설정이 아닌 **Gradle**로 전환해야 합니다.

* Gradle 설정
    1.  File -> Build Settings -> Player Settings -> Android -> Publishing Settings 에서 `Custom Gradle Template`을 활성화 하면 `Assets/Plugins/Android/mainTemplate.gradle` 파일이 생성이 됩니다.
        * ![unity_gradle.png](images/unity_gradle.png)
        * 기존에 사용중이던 mainTemplate.gradle 파일이 있는 경우는 생략할 수 있습니다.
    2.  mainTemplate.gradle의 주석을 제거합니다.
        ```gradle
        // ENERATED BY UNITY. REMOVE THIS COMMENT TO PREVENT OVERWRITING WHEN EXPORTING AGAIN
        ```
    3.  mainTemplate.gradle에서 dependencies를 추가합니다.
        ```gradle
        dependencies {
            implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.3.72'
        }
        ```
        * 다른 패키지에서 이미 추가하고 있는 경우 해당 과정을 제외할 수 있습니다.

### iOS
* Other Linker Flags 설정
    * Xcode Target에서 Build Settings > Linking > Other Linker Flags에 -ObjC를 추가해야 합니다.

## 🔨 API

### ShowUrl

WebView를 표시합니다.

**Required 파라미터**
* url : 파라미터로 전송되는 url은 유효한 값이어야 합니다.
* openCallback : WebView가 오픈될 때 성공여부를 콜백으로 알려 줍니다.

**Optional 파라미터**
* configuration : GpmWebViewRequest.Configuration으로 WebView의 옵션을 변경 할 수 있습니다.
* closeCallback : WebView가 종료될 때 사용자에게 콜백으로 알려 줍니다.
* schemeList : 사용자가 받고 싶은 커스텀 Scheme 목록을 지정합니다.
    * "https://"를 입력하면 "https://"로 시작하는 모든 url을 schemeEvent로 받을 수 있습니다.
    * schemeEvent로 받은 scheme은 redirect 되지 않습니다.
* schemeEvent : schemeList로 지정한 커스텀 Scheme을 포함하는 url을 콜백으로 알려 줍니다.

#### Configuration

| Parameter | Values | Description |
| ------------------------ | ---------------------------------------- | --------------------------- |
| title                    | string                                   | WebView의 제목                 |
| orientation       | ScreenOrientation.Unknown    | 미지정(Device 설정) |
|                          | ScreenOrientation.Portrait       | 세로 모드                       |
|                          | ScreenOrientation.PortraitUpsideDown      | 뒤집힌 세로모드                      |
|                          | ScreenOrientation.LandscapeLeft</br>ScreenOrientation.Landscape | 가로 모드              |
|                          | ScreenOrientation.LandscapeRight | 가로 모드를 180도 회전              |
|                          | ScreenOrientation.AutoRotation | 자동              |
| contentMode</br>(iOS only)              | GamebaseWebViewContentMode.RECOMMENDED        | 현재 플랫폼 추천 브라우저    |
|                          | GamebaseWebViewContentMode.MOBILE             | 모바일 브라우저            |
|                          | GamebaseWebViewContentMode.DESKTOP            | 데스크탑 브라우저          |

**API**
```cs
static void ShowUrl(
    string url,
    GpmWebViewRequest.Configuration configuration,
    GpmWebViewCallback.GpmWebViewErrorDelegate openCallback,
    GpmWebViewCallback.GpmWebViewErrorDelegate closeCallback,
    List<string> schemeList,
    GpmWebViewCallback.GpmWebViewDelegate<string> schemeEvent)
```

**Example**

```cs
public void ShowUrl()
{
    GpmWebView.ShowUrl(
        "https://www.nhn.com",
        new GpmWebViewRequest.Configuration() {
            title = "WebView Title",
            orientation = ScreenOrientation.AutoRotation,
            contentMode = GpmWebViewContentMode.MOBILE// iOS only
        },
        OnOpenCallback,
        OnCloseCallback,
        new List<string>()
        {
            "USER_ CUSTOM_SCHEME"
        },
        OnSchemeEvent);
}

private void OnOpenCallback(GpmWebViewError error)
{
    // TODO
}

private void OnCloseCallback(GpmWebViewError error)
{
    // TODO
}

private void OnSchemeEvent(string data, GpmWebViewError error)
{
    // TODO
}
```

### Close

다음 API를 이용하여 보여지고 있는 WebView를 닫을 수 있습니다.

**API**
```cs
static void Close()
```

**Example**

```cs
public void Close()
{
    GpmWebView.Close();
}
```