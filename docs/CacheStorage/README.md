# CacheStorage

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [스펙](#스펙)
* [API](#api)
* [Release notes](./ReleaseNotes.md)

## 개요

* CacheStorage는 Unity에서 웹 통신을 할 때 Cache를 지원해 성능을 개선할 수 있는 서비스입니다.

## 스펙

### Unity 지원 버전

* 2018.4.0 이상

## API

### RequestHttpCache

url로 데이터를 요청합니다.
캐시 된 데이터와 웹 데이터가 동일한 데이터인 경우 캐시 된 데이터를 사용합니다.

**API**
```cs
public static CacheInfo RequestHttpCache(string url, Action<Result> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestHttpCache(url, (result) =>
    {
        if (result.success == true)
        {
            bytes[] data = result.data;
        }
    });
}
```

### RequestLocalCache

url로 이미 캐시 된 데이터를 요청합니다. 
캐시 되어있지 않은 경우 실패합니다.

**API**
```cs
public static CacheInfo RequestLocalCache(string url, Action<Result> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestLocalCache(url, (result) =>
    {
        if (result.success == true)
        {
            bytes[] data = result.data;
        }
    });
}
```

### GetCachedTexture

url로 이미 캐시 된 텍스처를 요청합니다.
앱 실행 후 로드한 텍스처라면 재사용합니다.

**API**
```cs
public static CacheInfo GetCachedTexture(string url, Action<CachedTexture> onResult)
```

**Example**
```cs

public void Something()
{
    string url;
    CacheInfo cacheInfo = GpmCacheStorage.GetCachedTexture(url, (cachedTexture) =>
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

**API**
```cs
public static CacheInfo RequestTexture(string url, Action<CachedTexture> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    CacheInfo cacheInfo = GpmCacheStorage.RequestTexture(url, (cachedTexture) =>
    {
        if (cachedTexture != null)
        {
            Texture texture = cachedTexture.texture;
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
public long GetCacheCount()
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

### SetMaxSize

관리할 최대 캐시 용량을 설정할 수 있습니다.
* size
    * 기본값은 0입니다.
    * 0일 때 무제한 저장합니다.
* applayStorage
    * true 일 때 저장소의 용량 크기를 조절합니다
    * false 일 때 설정값만 수정되고 파일이 추가될 때 적용됩니다.

**API**
```cs
public static void SetMaxSize(long size = 0, bool applyStorage = true)
```

**Example**
```cs
public void Something()
{
    long maxSize = 10 * 1024 * 1024; // 10 MB
    bool applayStorage = true; // 저장소 적용(자동 삭제)
    GpmCacheStorage.SetMaxSize(maxSize, applayStorage);
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

### SetMaxCount

관리할 최대 캐시 개수를 설정할 수 있습니다.
* count
    * 기본값은 0입니다.
    * 0일 때 무제한 저장합니다.
* applayStorage
    * true 일 때 저장소의 용량 크기를 조절합니다
    * false 일 때 설정값만 수정되고 파일이 추가될 때 적용됩니다.

**API**
```cs
public static void SetMaxCount(int count = 0, bool applyStorage = true)
```

**Example**
```cs
public void Something()
{
    int maxCount = 50000;
    bool applayStorage = true; // 저장소 적용(자동 삭제)
    GpmCacheStorage.SetMaxCount(maxCount, applayStorage);
}
```

### ClearCache

관리 중인 캐시를 제거합니다.

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

### GetCachePath

관리되는 캐시의 경로를 알 수 있습니다.

**API**
```cs
public static string GetCachePath()
```

**Example**
```cs
public string GetCachePath()
{
    return GpmCacheStorage.GetCachePath();
}
```

### SetCachePath

관리되는 캐시의 경로를 설정합니다.
기본값은 Application.temporaryCachePath입니다.

**API**
```cs
public static void SetCachePath(string path)
```

**Example**
```cs
public void SetCachePath()
{
    string path = Application.temporaryCachePath;
    GpmCacheStorage.SetCachePath(path);
}
```


### GetReRequestTime

웹캐시 재요청 시간을 알 수 있습니다.

**API**
```cs
public static long GetReRequestTime()
```

**Example**
```cs
public long GetReRequestTime()
{
    return GpmCacheStorage.GetReRequestTime();
}
```

### SetReRequestTime

웹캐시 재요청 시간을 정할 수 있습니다.
기본값은 0입니다. 단위는 Tick입니다.


**API**
```cs
public static void SetReRequestTime(long value)
```

**Example**
```cs
public void SetReRequestTime()
{
    long reRequestTime = TimeSpan.TicksPerHour * 4;
    GpmCacheStorage.SetReRequestTime(reRequestTime);
}
```
