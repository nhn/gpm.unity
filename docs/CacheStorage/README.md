# CacheStorage

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [설치](#설치)
* [스펙](#스펙)
* [API](#api)
* [Release notes](./ReleaseNotes.md)

## 개요

* CacheStorage는 Unity에서 웹 통신을 할 때 Cache를 지원합니다.
* Cache를 이용하여 통신을 할 때 받은 데이터를 재사용하여 성능을 개선할 수 있습니다.

### 성능 향상

네트워크 통신을 할 때 HTTP 기반으로 콘텐츠를 저장하고 재사용합니다.
이때 콘텐츠가 수정되지 않은 경우에는 응답에 콘텐츠를 포함하지 않기 때문에 전송 속도가 크게 향상됩니다

![](Images/1.png)

* CacheStorage 샘플 기반 성능 테스트
    * UnityWebRequest: 28ms
    * WebCache: 14ms
    * Local: 1ms 

웹 캐시를 사용했을 때 일반적인 통신보다 2배 정도 빨라진 것을 확인할 수 있습니다.

### 간편한 사용
관리 포인트가 URL 하나로 일원화되어 간편합니다.

콘텐츠를 재사용 하는 경우 속도가 매우 빠릅니다. 동시에 최신 콘텐츠의 데이터 관리도 필요합니다.
웹 캐시를 사용하게 되면 동일한 url로 최신 콘텐츠인지 검증하며 재사용할 수 있어 간편해집니다.

### 용량 관리
캐시를 관리하여 용량을 제어할 수 있습니다.

![](Images/CacheStorage_logic.png)

1. 실시간 관리
* 오랫동안 사용되지 않는 콘텐츠를 실시간으로 제거해 줍니다.
* UnusedPeriodTime와 RemoveCycle를 둘 다 설정해야 동작합니다.
    * UnusedPeriodTime
        * 설정한 시간(초) 동안 사용하지 않은 캐시를 지워줍니다.
    * RemoveCycle
        * 제거되는 캐시들을 성능에 영향이 가지 않도록 설정한 시간(초)마다 하나씩 제거합니다.

2. 조건 관리
* 새로운 콘텐츠를 받을 때 설정한 용량, 개수가 넘지 않도록 제거해 줍니다.
* 우선순위가 낮은 캐시부터 제거해 줍니다.
    * MaxCount
        * 관리되는 캐시가 설정한 개수가 넘으면 우선순위가 낮은 것부터 지워줍니다.
    * MaxSize
        * 관리되는 캐시가 설정한 용량이 넘으면 우선순위가 낮은 것부터 지워줍니다.
    

## 설치

1. [Game Package Manger 설치](https://assetstore.unity.com/packages/tools/utilities/game-package-manager-147711)
2. 실행 : [Unity Menu > Tools > GPM > Manager](https://github.com/nhn/gpm.unity#%EC%8B%A4%ED%96%89)
3. 서비스 설치 : CacheStorage

## 스펙

### Unity 지원 버전

* 2019.4.0 이상

## 사용 방법

1. using Gpm.CacheStorage를 선언합니다.
2. 대부분의 기능은 GpmCacheStorage에 정의되어 있습니다.
3. GpmCacheStorage.Initialize를 사용하여 초기화합니다.
4. GpmCacheStorage.Request를 사용하여 Cache를 요청합니다.

### NameSpace
```cs
using Gpm.CacheStorage;
```

### Initialize
CacheStorage를 사용하기 위해서는 반드시 초기화를 해야 합니다.
* GpmCacheStorage.Initialize를 호출합니다.

CacheStorage에 사용될 매개변수를 설정합니다.

* maxCount
    * 설정한 최대 개수가 넘으면 우선순위가 낮은 캐시부터 지워줍니다.
    * 0으로 설정 시 무제한입니다.
* maxSize
    * 설정한 최대 용량이 넘으면 우선순위가 낮은 캐시부터 지워줍니다.
    * 0으로 설정 시 무제한입니다.
* reRequestTime
    * 요청할 때 설정한 시간(초)이 지난 캐시는 재검증합니다.
    * 0으로 설정 시 요청 시간 기반으로 재검증하지 않습니다.
* defaultRequestType
    * 요청할 때 설정한 타입 기반으로 재검증합니다.
        * ALWAYS
            * 요청할 때마다 재검증합니다.
        * FIRSTPLAY
            * 앱이 재실행 될 때마다 재검증합니다, 유효기간이 끝났을때도 재검증합니다.
        * Once
            * 재사용 하고 유효기간이 끝났을때 재검증합니다.
        * LOCAL
            * 저장된 캐시를 사용합니다.
* unusedPeriodTime
    * 설정한 시간(초) 동안 사용하지 않은 캐시를 지워줍니다.
    * unusedPeriodTime 또는 removeCycle가 0으로 설정 시 실시간 제거를 하지 않습니다.
* removeCycle
    * 제거되는 캐시들을 성능에 영향이 가지 않도록 설정한 시간(초)마다 하나씩 제거합니다.
    * unusedPeriodTime 또는 removeCycle가 0으로 설정 시 실시간 제거를 하지 않습니다.

```cs
using Gpm.CacheStorage;

public void Something()
{
    int maxCount = 10000;
    int maxSize = 5 * 1024 * 1024; // 5 MB
    double reRequestTime = 30 * 24 * 60 * 60; // 30 Days
    CacheRequestType defaultRequestType = CacheRequestType.FIRSTPLAY;
    double unusedPeriodTime = 365 * 24 * 60 * 60; // 1 Years
    double removeCycle = 1; // 1 Seconds
             
    GpmCacheStorage.Initialize(maxCount, maxSize, reRequestTime, defaultRequestType, unusedPeriodTime, removeCycle);
}
```

### Request
Request를 통해 url의 데이터를 요청합니다.
* 데이터는 cache로 저장되며 같은 url을 호출할 때 재사용 합니다.
* CacheRequestType을 통해 언제 서버에 검증할 것인지 정의할 수 있습니다.
* 서버에 검증할 때 동일한 데이터일 경우 다시 받지 않고 캐시를 재사용합니다.

```cs
using Gpm.CacheStorage;

public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### GpmCacheResult
캐시 된 데이터의 결괏값입니다. 캐시 정보와 데이터를 반환합니다.
* IsSuccess 통해 성공 여부를 받아올 수 있습니다.
* 기본적으로 데이터는 Data로 저장됩니다.
* Text나 Json은 인코딩을 통해 변환할 수 있으며 기본값은 utf8입니다.

```cs
bool IsSuccess() // 결과 성공 여부를 반환합니다.
CacheInfo Info; // 캐시 정보를 반환합니다.
byte[] Data;  // 캐시 데이터를 반환합니다.
string Text;  // utf8로 인코딩된 데이터를 반환합니다.

string GetTextData() // utf8로 인코딩된 데이터를 반환합니다.
string GetTextData(Encoding encoding) // 인코딩된 데이터를 반환합니다.

T GetJsonData<T>() // utf8로 인코딩된 json 데이터를 반환합니다.
T GetJsonData<T>(Encoding encoding) // utf8로 인코딩된 json 데이터를 반환합니다.
```

```cs
public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        // success
        if (result.IsSuccess() == true)
        {
            // date
            bytes[] data = result.Data;

            // text - Encoding.UTF8
            string text = result.Text;

            // text - Encoding.UTF8
            text = result.GetTextData();

            // text - Encoding.Default
            text = result.GetTextData(Encoding.Default);    

            // json - Encoding.UTF8
            JsonClass json = result.GetJsonData<JsonClass>();

            // json - Encoding.Default
            json = result.GetJsonData<JsonClass>(Encoding.Default);           
        }
    });
}
```

### CacheRequestOperation
캐시를 요청할 때 반환 값입니다. 캐시 요청 상태를 알 수 있습니다.

```cs
bool keepWaiting() // 코루틴에서 대기 할 것인지를 반환합니다.
void Cancel() // 요청을 취소합니다. 취소한 요청은 콜백이 전달되지 않습니다.
```

#### 코루틴 대기하기
CacheRequestOperation를 이용하여 코루틴에서 대기할 수 있습니다.
```cs
using Gpm.CacheStorage;

public IEnumerator Something()
{
    bytes[] data;
    string url;
    yield return GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            data = result.Data;
        }
    });
}
```

#### 요청 취소하기
요청을 취소하여 콜백을 받지 않을 수 있습니다.
```cs
using Gpm.CacheStorage;

public IEnumerator Something()
{
    bytes[] data;
    string url;
    CacheRequestOperation op = GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            data = result.Data;
        }
    });

    // Cancel
    op.Cancel();

    yield return op;
}
```

### 텍스처 캐싱 요청
RequestTexture를 통해 캐시된 텍스처를 요청할 수 있습니다.
* 앱 실행 후 로드한 텍스처라면 재사용합니다.
* 캐시된 데이터와 웹 데이터가 동일한 데이터인 경우 캐시된 텍스처를 로드하여 사용합니다.

```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestTexture(url, (CachedTexture cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            Texture texture = cachedTexture.texture;
        }
    });
}
```

```cs
public IEnumerator Something()
{
    CachedTexture cachedTexture;
    string url;
    yield return GpmCacheStorage.RequestTexture(url, (CachedTexture recvCachedTexture) =>
    {
        cachedTexture = recvCachedTexture;
    });

    if (cachedTexture != null)
    {
        Texture texture = cachedTexture.texture;
    }
}
```

### CachedTexture
캐시 된 텍스쳐의 결괏값입니다. 캐시 정보를 반환합니다.
* 캐시 된 텍스쳐를 받아올 수 있습니다.
* updateData를 통해 텍스쳐 변경 여부를 알 수 있습니다.

```cs
CacheInfo info // 캐시 정보를 반환합니다.
Texture2D texture; // 결과 텍스쳐를 반환합니다.
bool requested;  // true일 때 웹에서 새로 받은 요청입니다.
bool updateData;  // true일 때 새롭게 업데이트된 텍스쳐입니다.

void DestroyTexture() // 텍스쳐를 파괴하고 관리되는 텍스쳐에서도 제외합니다.
void ReleaseCache() // 관리되는 텍스쳐에서 제외합니다. 텍스쳐를 파괴하지는 않습니다.
```

```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestTexture(url, (CachedTexture cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            // texture
            Texture texture = cachedTexture.texture;

            // requested
            bool requested = cachedTexture.requested;

            // updateData
            bool updateData = cachedTexture.updateData;

            // DestroyTexture
            cachedTexture.DestroyTexture();

            // ReleaseCache
            cachedTexture.ReleaseCache();
        }
    });
}
```

## 더 효과적인 웹 캐시 사용
웹 캐시를 사용하면 일반 요청보다 속도가 2배 정도 빠릅니다.
로컬에서 불러오는 것은 더욱 빠르지만 최신 상태 여부를 확인할 수 없습니다.

![](Images/3.png)

이러한 특성을 활용하여 필요할 때만 검증하면 웹 캐시를 더욱 효과적으로 사용할 수 있습니다.

### 웹 캐시 검증 전략

보안이 중요하거나 지속적인 갱신이 필요할 경우는 일반적인 네트워크 통신을 이용해 무결성을 보장합니다.
그리고 콘텐츠가 성능이 더 중요한지 무결성이 더 중요한지에 따라 검증 전략을 달리하면 성능을 더욱 향상시킬 수 있습니다.

![](Images/4.png)

CacheStorage에서는 아래와 같이 4가지 검증 전략을 지원하고 있습니다.

### CacheRequestType
캐시 된 데이터를 언제 서버에 다시 검증할지를 결정할 수 있습니다.
재검증이 많을수록 무결성을 보장해 주며 재사용이 많을수록 성능이 향상됩니다.

* ALWAYS
    * 요청할 때마다 재검증합니다.
    * GpmCacheStorage.RequestHttpCache과 동일합니다.
* FIRSTPLAY
    * 앱이 재실행 될 때마다 재검증합니다, 유효기간이 끝났을 때도 재검증합니다.
    * 만료되거나 ReRequestTime 설정에 따라 재검증합니다.
* ONCE
    * 유효기간이 끝났을 때 재검증합니다.
    * 만료되거나 ReRequestTime 설정에 따라 재검증합니다.
* LOCAL
    * 캐시 된 데이터를 사용합니다.
    * GpmCacheStorage.RequestLocalCache과 동일합니다.

#### Request 할 때 인자를 넣어서 요청할 수 있습니다.
* 인자를 사용하지 않으면 Initialize에서 설정한 기본값을 사용합니다.

```cs
using Gpm.CacheStorage;

public void Something()
{
    // 요청할 때마다 재검증
    string url;
    CacheRequestType requestType = CacheRequestType.ALWAYS;
    GpmCacheStorage.Request(url, requestType, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### ReRequestTime
FIRSTPLAY, ONCE는 받아온 데이터 기반으로 캐시가 만료되기 전까지 재사용합니다.
그러나 클라 내에서 재검증 요청 주기를 설정할 수 있습니다.
* 설정된 초가 지나면 재 호출 시 서버에 다시 검증합니다.
* 0으로 설정될 때 재요청을 하지 않습니다.

#### Request 할 때 인자를 넣어서 사용할 수 있습니다.
* 인자가 0이거나 사용하지 않으면 Initialize에서 설정한 기본값을 사용합니다.

```cs
using Gpm.CacheStorage;

public void Something()
{
    // 요청한지 5분이 지난 캐시는 서버에 재검증
    string url;
    double fiveMinutes = 5 * 60;
    GpmCacheStorage.Request(url, fiveMinutes, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

## Viewer
CacheStorage의 캐시 정보를 확인해 볼 수 있습니다.

* 사용 방법
    * 메뉴의 GPM/CacheStorage/Viewer 를 통해 오픈 가능합니다.

![](Images/viewer.png)

### 1. Management
관리되는 캐시 메뉴입니다.

* Size : 현재 캐시 용량 / 최대 용량 (byte 단위)
    * 현재 Cache 용량과 설정된 최대 용량입니다.
    * 최대 용량이 넘지 않게 유지해줍니다.
* Count : 현재 캐시 개수 / 최대 개수
    * 현재 Cache 개수와 설정된 최대 개수입니다.
    * 최대 개수가 넘지 않게 유지해줍니다.

### 2. Request Info
캐시를 요청할 때 사용되는 정보입니다.

* Default RequestType
    * 요청할 때 설정한 타입 기반으로 재검증합니다.
        * ALWAYS
            * 요청할 때마다 재검증합니다.
        * FIRSTPLAY
            * 앱이 재실행 될 때마다 재검증합니다, 유효기간이 끝났을 때도 재검증합니다.
        * Once
            * 유효기간이 끝났을 때 재검증합니다.
        * LOCAL
            * 저장된 캐시를 사용합니다.
* ReRequest
    * 요청할 때 설정한 시간(초)이 지난 캐시는 재검증합니다.
    * 0으로 설정 시 요청 시간 기반으로 재검증하지 않습니다.

### 3. Auto Remove
오랫동안 사용되지 않는 콘텐츠를 실시간으로 제거해 줍니다.
UnusedPeriodTime와 RemoveCycle를 둘 다 설정해야 동작합니다.

* UnusedPeriodTime
    * 설정한 시간(초) 동안 사용하지 않은 캐시를 지워줍니다.
    * unusedPeriodTime 또는 removeCycle가 0일 때 실시간 제거를 하지 않습니다.
* RemoveCycle
    * 제거되는 캐시들을 성능에 영향이 가지 않도록 설정한 시간(초)마다 하나씩 제거합니다.
    * unusedPeriodTime 또는 removeCycle가 0일 때 실시간 제거를 하지 않습니다.

### 4. 캐시 데이터 리스트
관리하고 있는 캐시 데이터 리스트입니다.

* Name : 캐시 이름
* Url : 캐시 경로
* Size : 캐시 크기 (byte 단위)
* Exfires : 유효기간까지 남은 시간
* Remain : 캐시 검증까지 남은 시간
    * 남은 시간이 지나면 재검증합니다.
    * 유효기간까지 남은 시간과 ReRequest(초 단위) 시간 중 짧은 시간
* Remove : 제거될 때까지 남은 시간
    * 남은 시간 동안 사용하지 않으면 제거됩니다.
    * 사용한 시간 / UnusedPeriodTime로 설정된 시간 (초 단위)
    * unusedPeriodTime 또는 removeCycle가 0일 때 실시간 제거를 하지 않습니다.

### 5. 캐시 상세 정보
리스트에서 선택된 캐시 데이터 상세 정보입니다.

## API

### Initialize
CacheStorage를 사용하기 위해서는 반드시 초기화를 해야 합니다.

* maxCount
    * 설정한 최대 개수가 넘으면 우선순위가 낮은 캐시부터 지워줍니다.
    * 0으로 설정 시 무제한입니다.
* maxSize
    * 설정한 최대 용량이 넘으면 우선순위가 낮은 캐시부터 지워줍니다.
    * 0으로 설정 시 무제한입니다.
* reRequestTime
    * 요청할 때 설정한 시간(초)이 지난 캐시는 재검증합니다.
    * 0으로 설정 시 요청 시간 기반으로 재검증하지 않습니다.
* defaultRequestType
    * 요청할 때 설정한 타입 기반으로 재검증합니다.
        * ALWAYS
            * 요청할 때마다 재검증합니다.
        * FIRSTPLAY
            * 앱이 재실행 될 때마다 재검증합니다, 유효기간이 끝났을 때도 재검증합니다.
        * Once
            * 재사용 하고 유효기간이 끝났을 때 재검증합니다.
        * LOCAL
            * 저장된 캐시를 사용합니다.
* unusedPeriodTime
    * 설정한 시간(초) 동안 사용하지 않은 캐시를 지워줍니다.
    * unusedPeriodTime 또는 removeCycle가 0으로 설정 시 실시간 제거를 하지 않습니다.
* removeCycle
    * 제거되는 캐시들을 성능에 영향이 가지 않도록 설정한 시간(초)마다 하나씩 제거합니다.
    * unusedPeriodTime 또는 removeCycle가 0으로 설정 시 실시간 제거를 하지 않습니다.

**API**
```cs
public static void Initialize(int maxCount, int maxSize, double reRequestTime, CacheRequestType defaultRequestType, double unusedPeriodTime, double removeCycle)
```

**Example**
```cs
public void Something()
{
    int maxCount = 10000;
    int maxSize = 5 * 1024 * 1024; // 5 MB
    double reRequestTime = 30 * 24 * 60 * 60; // 30 Days
    CacheRequestType defaultRequestType = CacheRequestType.FIRSTPLAY;
    double unusedPeriodTime = 365 * 24 * 60 * 60; // 1 Years
    double removeCycle = 1; // 1 Seconds
             
    GpmCacheStorage.Initialize(maxCount, maxSize, reRequestTime, defaultRequestType, unusedPeriodTime, removeCycle);
}
```

### Request

url로 데이터를 요청합니다.
캐시된 데이터와 웹 데이터가 동일한 데이터인 경우 캐시된 데이터를 사용합니다.

* url
    * 요청할 캐시 경로입니다.
* requestType
    * 캐시 된 데이터를 언제 서버에 다시 검증할지를 결정하는 타입입니다.
    * 인자를 사용하지 않으면 Initialize에서 설정한 기본값을 사용합니다.
* reRequestTime
    * 함수 별로 재검증 요청 주기를 설정할 수 있습니다.
    * 기준은 초입니다. 10으로 설정한 다면 10초가 지난 캐시는 재검증합니다.
    * 인자가 0이거나 사용하지 않으면 Initialize에서 설정한 기본값을 사용합니다.

**API**
```cs
public static CacheRequestOperation Request(string url, Action<GpmCacheResult> onResult)
```
```cs
public static CacheRequestOperation Request(string url, CacheRequestType requestType, Action<GpmCacheResult> onResult)
```
```cs
public static CacheRequestOperation Request(string url, double reRequestTime, Action<GpmCacheResult> onResult)
```
```cs
public static CacheRequestOperation Request(string url, CacheRequestType requestType, double reRequestTime, Action<GpmCacheResult> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

```cs
public IEnumerator Something()
{
    string url;
    bytes[] data;
    yield return GpmCacheStorage.Request(url, CacheRequestType.ONCE, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            data = result.Data;
        }
    });
}
```

### GpmCacheResult
캐시 된 데이터의 결괏값입니다. 캐시 정보와 데이터를 반환합니다.
* IsSuccess 통해 성공 여부를 받아올 수 있습니다.
* 기본적으로 데이터는 Data로 저장됩니다.
* Text나 Json은 인코딩을 통해 변환할 수 있으며 기본값은 utf8입니다.

**API**
```cs
bool IsSuccess() // 결과 성공 여부를 반환합니다.
CacheInfo Info; // 캐시 정보를 반환합니다.
byte[] Data;  // 캐시 데이터를 반환합니다.
string Text;  // utf8로 인코딩된 데이터를 반환합니다.

string GetTextData() // utf8로 인코딩된 데이터를 반환합니다.
string GetTextData(Encoding encoding) // 인코딩된 데이터를 반환합니다.

T GetJsonData<T>() // utf8로 인코딩된 json 데이터를 반환합니다.
T GetJsonData<T>(Encoding encoding) // utf8로 인코딩된 json 데이터를 반환합니다.
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        // success
        if (result.IsSuccess() == true)
        {
            // date
            bytes[] data = result.Data;

            // text - Encoding.UTF8
            string text = result.Text;

            // text - Encoding.UTF8
            text = result.GetTextData();

            // text - Encoding.Default
            text = result.GetTextData(Encoding.Default);    

            // json - Encoding.UTF8
            JsonClass json = result.GetJsonData<JsonClass>();

            // json - Encoding.Default
            json = result.GetJsonData<JsonClass>(Encoding.Default);           
        }
    });
}
```

### CacheRequestOperation
캐시를 요청할 때 반환 값입니다. 캐시 요청 상태를 알 수 있습니다.
* 코루틴에서 대기할 수 있습니다.
* 캐시 요청을 취소할 수도 있습니다.

**API**
```cs
bool keepWaiting() // 코루틴에서 대기 할 것인지를 반환합니다.
void Cancel() // 요청을 취소합니다. 취소한 요청은 콜백이 전달되지 않습니다.
```

**Example**
```cs
using Gpm.CacheStorage;

public IEnumerator Something()
{
    bytes[] data;
    string url;
    CacheRequestOperation op = GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            data = result.Data;
        }
    });

    while(op.keepWaiting() == true)
    {
        yield return null;
    }
}
```

```cs
public IEnumerator Something()
{
    bytes[] data;
    string url;
    CacheRequestOperation op = GpmCacheStorage.Request(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            data = result.Data;
        }
    });

    // Cancel
    op.Cancel();

    yield return op;
}
```

### RequestHttpCache

url로 데이터를 요청합니다.
캐시 된 데이터와 웹 데이터가 동일한 데이터인 경우 캐시 된 데이터를 사용합니다.

**API**
```cs
public static CacheRequestOperation RequestHttpCache(string url, Action<GpmCacheResult> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestHttpCache(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

```cs
public IEnumerator Something()
{
    string url;
    bytes[] data;
    yield return GpmCacheStorage.RequestHttpCache(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            data = result.Data;
        }
    });
}
```

### RequestLocalCache

url로 이미 캐시 된 데이터를 요청합니다. 
캐시 되어있지 않은 경우 실패합니다.

**API**
```cs
public static CacheRequestOperation RequestLocalCache(string url, Action<GpmCacheResult> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestLocalCache(url, (GpmCacheResult result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### GetCachedTexture

url로 이미 캐시 된 텍스처를 요청합니다.
앱 실행 후 로드한 텍스처라면 재사용합니다.

**API**
```cs
public static CacheRequestOperation GetCachedTexture(string url, Action<CachedTexture> onResult)
```

**Example**
```cs

public void Something()
{
    string url;
    GpmCacheStorage.GetCachedTexture(url, (CachedTexture cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            Texture texture = cachedTexture.texture;
        }
    });
}
```

### RequestTexture

url로 캐시 된 데이터를 요청합니다. 
앱 실행 후 로드한 텍스처라면 재사용합니다.
캐시 된 데이터와 웹 데이터가 동일한 데이터인 경우 캐시 된 텍스처를 로드하여 사용합니다.

* url
    * 요청할 캐시 경로입니다.
* requestType
    * 캐시 된 데이터를 언제 서버에 다시 검증할지를 결정하는 타입입니다.
    * 인자를 사용하지 않으면 Initialize에서 설정한 기본값을 사용합니다.
* reRequestTime
    * 함수 별로 재검증 요청 주기를 설정할 수 있습니다.
    * 마지막 검증한 이후 설정한 시간(초 단위)가 지나면 재검증합니다.
    * 인자가 0이거나 사용하지 않으면 Initialize에서 설정한 기본값을 사용합니다.
* preLoad
    * 웹에 검증하기 전에 미리 저장된 캐시를 읽어옵니다.
    * 검증 이후 콘텐츠가 바뀌었을 경우 콜백이 다시 호출됩니다.

**API**
```cs
public static CacheRequestOperation RequestTexture(string url, Action<CachedTexture> onResult)
```

```cs
public static CacheRequestOperation RequestTexture(string url, bool preLoad, Action<CachedTexture> onResult)
```

```cs
public static CacheRequestOperation RequestTexture(string url, CacheRequestType requestType, Action<CachedTexture> onResult)
```

```cs
public static CacheRequestOperation RequestTexture(string url, CacheRequestType requestType, bool preLoad, Action<CachedTexture> onResult)
```

```cs
public static CacheRequestOperation RequestTexture(string url, double reRequestTime, Action<CachedTexture> onResult)
```

```cs
public static CacheRequestOperation RequestTexture(string url, double reRequestTime,  bool preLoad, Action<CachedTexture> onResult)
```

```cs
public static CacheRequestOperation RequestTexture(string url, CacheRequestType requestType, double reRequestTime, bool preLoad, Action<CachedTexture> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestTexture(url, (CachedTexture cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            Texture texture = cachedTexture.texture;
        }
    });
}
```

```cs
public IEnumerator Something()
{
    string url;
    Texture texture;
    yield return GpmCacheStorage.RequestTexture(url, true, (CachedTexture cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            texture = cachedTexture.texture;
        }
    });
}
```

### CachedTexture

캐시 된 텍스쳐의 결괏값입니다. 캐시 정보를 반환합니다.
* 캐시 된 텍스쳐를 받아올 수 있습니다.
* updateData를 통해 텍스쳐 변경 여부를 알 수 있습니다.

**API**
```cs
CacheInfo info // 캐시 정보를 반환합니다.
Texture2D texture; // 결과 텍스쳐를 반환합니다.
bool requested;  // true일 때 웹에서 새로 받은 요청입니다.
bool updateData;  // true일 때 새롭게 업데이트된 텍스쳐입니다.

void DestroyTexture() // 텍스쳐를 파괴하고 관리되는 텍스쳐에서도 제외합니다.
void ReleaseCache() // 관리되는 텍스쳐에서 제외합니다. 텍스쳐를 파괴하지는 않습니다.
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestTexture(url, (CachedTexture cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            // texture
            Texture texture = cachedTexture.texture;

            // requested
            bool requested = cachedTexture.requested;

            // updateData
            bool updateData = cachedTexture.updateData;

            // DestroyTexture
            cachedTexture.DestroyTexture();

            // ReleaseCache
            cachedTexture.ReleaseCache();
        }
    });
}
```

### GetCacheSize

관리 중인 캐시 용량을 알 수 있습니다.

**API**
```cs
public static long GetCacheSize()
```

**Example**
```cs
public long GetCacheSize()
{
    return GpmCacheStorage.GetCacheSize();
}
```

### GetMaxSize

관리할 최대 캐시 용량을 알 수 있습니다.

**API**
```cs
public static long GetMaxSize()
```

**Example**
```cs
public long GetMaxSize()
{
    return GpmCacheStorage.GetMaxSize();
}
```

### GetCacheCount

관리 중인 캐시 수를 알 수 있습니다.

**API**
```cs
public static int GetCacheCount()
```

**Example**

```cs
public int GetCacheCount()
{
    return GpmCacheStorage.GetCacheCount();
}
```

### GetMaxCount

관리할 최대 캐시 개수를 알 수 있습니다.

**API**
```cs
public static int GetMaxCount()
```

**Example**
```cs
public int GetMaxCount()
{
    return GpmCacheStorage.GetMaxCount();
}
```

### GetReRequestTime

웹캐시 재요청 시간을 알 수 있습니다.

**API**
```cs
public static double GetReRequestTime()
```

**Example**
```cs
public double GetReRequestTime()
{
    return GpmCacheStorage.GetReRequestTime();
}
```

### GetCacheRequestType

GpmCacheStorage.Request를 요청할 때 적용되는 CacheRequestType를 알 수 있습니다.

**API**
```cs
public static CacheRequestType GetCacheRequestType()
```

**Example**
```cs
public CacheRequestType GetCacheRequestType()
{
    return GpmCacheStorage.GetCacheRequestType();
}
```

### GetUnusedPeriodTime

불필요한 에셋의 삭제 기간을 알 수 있습니다.

**API**
```cs
public static double GetUnusedPeriodTime()
```

**Example**
```cs
public double GetUnusedPeriodTime()
{
    return GpmCacheStorage.GetUnusedPeriodTime();
}
```

### GetRemoveCycle

지연 삭제 주기를 알 수 있습니다.

**API**
```cs
public static double GetRemoveCycle()
```

**Example**
```cs
public double GetRemoveCycle()
{
    return GpmCacheStorage.GetRemoveCycle();
}
```

### ClearCache

관리 중인 모든 캐시를 제거합니다.

**API**
```cs
public static void ClearCache()
```

**Example**
```cs
public void ClearCache()
{
    GpmCacheStorage.ClearCache();
}
```

### RemoveCache

관리 중인 캐시를 제거합니다.

**API**
```cs
public static void RemoveCache()
```

**Example**
```cs
public bool RemoveCache()
{
    string url;
    if( GpmCacheStorage.RemoveCache(url) == true)
    {
        // removed
    }
}
```