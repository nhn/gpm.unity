# WebCacheImage

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [사용 방법](#사용-방법)
* [API](#api)

## 개요

URL을 이용하여 웹 이미지를 캐시 하여 이미지를 보여주는 컴포넌트입니다.

## 사용 방법
UI 오브젝트에 **WebCacheImage** 컴포넌트를 추가합니다.
* RawImage가 없다면 RawImage 컴포넌트도 같이 생성됩니다.
* RawImage가 있다면 RawImage 컴포넌트에 연동됩니다.

![WebCacheImage.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/WebCacheImage/images/WebCacheImage.png?raw=true)

1. Url: 이미지를 불러올 URL입니다.
2. Pre Load: 웹 요청을 통해 이미지를 얻을 경우 딜레이가 발생합니다. 캐시가 있을 경우 미리 불러옵니다.
3. Cache Config: 캐시 세부 설정
    * Request Type: 캐시 요청 타입 설정
    * Re Request Time: 캐시 최대 재검증 기간(초) 설정
    * Valid Cache Time
        * min: 최소 캐시 유효 기간(초)
        * max: 최대 캐시 유효 기간(초)
4. On Load Texture: Texture가 요청을 통해 로드되었을 때의 이벤트입니다.

### 캐시 세부 설정

WebCacheImage는 이미지 캐시 관리를 위해 CacheStorage를 사용합니다. 
* Cache Config를 통해 제어할 수 있습니다.
* 참조 : [더 효과적인 웹 캐시 사용](https://github.com/nhn/gpm.unity/tree/main/docs/CacheStorage#%EB%8D%94-%ED%9A%A8%EA%B3%BC%EC%A0%81%EC%9D%B8-%EC%9B%B9-%EC%BA%90%EC%8B%9C-%EC%82%AC%EC%9A%A9)

### 요청 헤더 설정

인자를 통해 헤더를 설정할 수 있습니다.

```cs
WebCacheImage cache;

Dictionary<string, string> header = new Dictionary<string, string>();
header.Add("key", "value");

cache.SetHeader(header);
```

## API

### SetUrl

이미지를 불러올 URL을 설정합니다.

```cs
void SetUrl(string url)
void SetUrl(string url, Dictionary<string, string> header)
```

**Example**
```cs
WebCacheImage cache;

string url = "url";

cache.SetUrl(url);
```

```cs
WebCacheImage cache;

string url = "url";
Dictionary<string, string> header = new Dictionary<string, string>();
header.Add("key", "value");

cache.SetUrl(url, header);
```

### SetLoadTextureEvent

이미지를 로드할 때 이벤트를 설정합니다.

```cs
void SetLoadTextureEvent(UnityAction<Texture> onListener)
```

**Example**
```cs
WebCacheImage cache;
cache.SetLoadTextureEvent(OnLoadTexture);

public void OnLoadTexture(Texture texture)
{
}
```

### AddLoadTextureEvent

이미지를 로드할 때 이벤트를 추가합니다.

```cs
void AddLoadTextureEvent(UnityAction<Texture> onListener)
```

**Example**
```cs
WebCacheImage cache;
cache.AddLoadTextureEvent(OnLoadTexture);

public void OnLoadTexture(Texture texture)
{
}
```

### CleatLoadTextureEvent

이미지를 로드할 때 이벤트를 초기화합니다.

```cs
void CleatLoadTextureEvent()
```

**Example**
```cs
WebCacheImage cache;
cache.CleatLoadTextureEvent();
```

### SetPreloadSetting

이미지를 요청할 때 미리 불러오는지 여부를 설정합니다.

```cs
void void SetPreloadSetting(bool preLoad) 
```

**Example**
```cs
WebCacheImage cache;

cache.SetPreloadSetting(true);
```

### SetHeader

이미지를 요청할 때 사용하는 헤더를 설정합니다.

```cs
void SetHeader(Dictionary<string, string> header)
```

**Example**
```cs
WebCacheImage cache;

Dictionary<string, string> header = new Dictionary<string, string>();
header.Add("key", "value");
    
cache.SetHeader(header);
```

### SetCacheConfig

이미지를 요청할 때 캐시 세부 설정을 합니다.

```cs
void SetCacheConfig(CacheRequestConfiguration config)
```

**Example**
```cs
WebCacheImage cache;

CacheRequestConfiguration cacheConfig = new CacheRequestConfiguration(
            CacheRequestType.ONCE, 
            60 * 60 * 2, 
            new CacheValidTime(60 * 5, 60 * 60 * 24 * 30)); 
    
cache.SetCacheConfig(cacheConfig);
```

### SetCacheRequestType

이미지를 요청할 때 캐시를 재검증하는 방법을 설정합니다.

```cs
void SetCacheRequestType(CacheRequestType requestType)
```

**Example**
```cs
WebCacheImage cache;

CacheRequestType requestType = CacheRequestType.FIRSTPLAY;
    
cache.SetCacheRequestType(requestType);
```

### SetCacheReRequestTime

이미지를 요청할 때 캐시를 재검증하는 시간을 설정합니다.

```cs
void SetCacheReRequestTime(double reRequestTime)
```

* 설정한 시간(초) 이후 이미지가 바뀌었는지 서버에 재검증합니다.
* 값이 0이라면 콘텐츠 서버에 설정된 유효기간에 따릅니다.
* 서버에 콘텐츠 유효기간과 비교해 더 빠른 시간에 재검증합니다.

**Example**
```cs
WebCacheImage cache;

double reRequestTime = 60 * 60 * 2; // 2 Hours
    
cache.SetCacheReRequestTime(reRequestTime);
```

### SetCacheValidMinTime

이미지 캐시의 최소 재사용 기간을 설정합니다.

```
public void SetCacheValidMinTime(double min)
```

* 최소 시간(초)을 설정하면 해당 시간까지 무조건 저장된 캐시를 읽습니다.
* 값이 0이라면 무시됩니다.

**Example**
```cs
WebCacheImage cache;

double validCacheMinTime = 60 * 5;  // 5 Minutes
    
cache.SetCacheValidMinTime(validCacheMinTime);
```

### SetCacheValidMaxTime

이미지 캐시의 최대 재사용 기간을 설정합니다.

```cs
public void SetCacheValidMaxTime(double max)
```

* 최대 시간(초)을 설정하면 해당 시간 이후 무조건 새로운 캐시를 다운로드합니다.
* 값이 0이라면 무시됩니다.

**Example**
```cs
WebCacheImage cache;

double validCacheMaxTime = 60 * 60 * 24 * 30; // 30 Days
    
cache.SetCacheValidMaxTime(validCacheMaxTime);
```

### SetCacheValidTime

이미지 캐시의 최대 및 최소 재사용 기간을 설정합니다.

```cs
void SetCacheValidTime(double min, double max)
```

* 최소 시간(초)을 설정하면 해당 시간까지 무조건 저장된 캐시를 읽습니다.
* 최대 시간(초)을 설정하면 해당 시간 이후 무조건 새로운 캐시를 다운로드합니다.
* 값이 0이라면 무시됩니다.

**Example**
```cs
WebCacheImage cache;

double validCacheMinTime = 60 * 5; // 5 Minutes
double validCacheMaxTime = 60 * 60 * 24 * 30; // 30 Days
    
cache.SetCacheValidTime(validCacheMinTime, validCacheMaxTime);
```

### GetURL

이미지를 불러올 URL을 얻습니다.

```cs
string GetURL()
```

### GetPreloadSetting

이미지를 요청할 때 미리 불러오는지 여부를 얻습니다.

```cs
bool GetPreloadSetting()  
```

### GetCacheRequestType

이미지를 요청할 때 캐시를 재검증하는 방법을 얻습니다.

```cs
CacheRequestType GetCacheRequestType()
```

### GetCacheReRequestTime

이미지를 요청할 때 캐시를 재검증하는 시간을 얻습니다.

```cs
double GetCacheReRequestTime()
```

### GetCacheValidMinTime

이미지 캐시의 최소 재사용 기간을 얻습니다.

```cs
double GetCacheValidMinTime()
```

### GetCacheValidMaxTime

이미지 캐시의 최대 재사용 기간을 얻습니다.

```cs
double GetCacheValidMaxTime()
```