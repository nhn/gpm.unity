# CacheStorage

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#overview)
* [Specification](#Specification)
* [API](#api)
* [Release notes](./ReleaseNotes.en.md)

## Overview

CacheStorage is a service that can improve performance by supporting Cache during web communication in Unity


## Specification

### Versions that support Unity

* 2018.4.0 or higher

## API

### RequestHttpCache

Request data by url.
If the cached data and the web data are the same data, the cached data is used.

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

Request already cached data by url.
Fails if not cached.

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

Request an already cached texture by url.
If the texture is loaded after running the app, it will be reused.

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

Request cached data by url.
If the texture is loaded after running the app, it will be reused.
If the cached data and web data are the same data, the cached texture is loaded and used.

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
Can see the amount of cache used.

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

Can See the maximum cache capacity to manage.

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

Can set the maximum cache capacity to manage.
* size
    * Default is 0.
    * When 0, unlimited storage.
* appplayStorage
    * When true, adjust the size of the storage capacity
    * When false, only the setting value is modified and applied when a file is added.

**API**
```cs
public static void SetMaxSize(long size = 0, bool applyStorage = true)
```

**Example**
```cs
public void Something()
{
    long maxSize = 10 * 1024 * 1024; // 10 MB
    bool applayStorage = true; // Apply Storage (Auto Remove)
    GpmCacheStorage.SetMaxSize(maxSize, applayStorage);
}
```

### GetCacheCount

Can see the number of caches used.

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

Can See the maximum number of caches to manage.

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

Can set the maximum number of caches to manage.
* count
    * Default is 0.
    * When 0, unlimited storage.
* appplayStorage
    * When true, adjust the size of the storage capacity
    * When false, only the setting value is modified and applied when a file is added.

**API**
```cs
public static void SetMaxCount(int count = 0, bool applyStorage = true)
```

**Example**
```cs
public void Something()
{
    int maxCount = 50000;
    bool applayStorage = true; // Apply Storage (Auto Remove))
    GpmCacheStorage.SetMaxCount(maxCount, applayStorage);
}
```

### ClearCache

Remove the managed cache.

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

Can know the path to the managed cache.

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

Sets the path to the managed cache.
The default is Application.temporaryCachePath .

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

 Can see the webcache re-request time.

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

Can set the webcache re-request time.
Default is 0. The unit is Tick.


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
