# CacheStorage

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#overview)
* [Specification](#Specification)
* [API](#api)
* [Release notes](./ReleaseNotes.en.md)

## Overview
* CacheStorage supports Cache when web communications are performed in Unity.
* Cache can be used to improve performance by reusing the data received when communicating.

## Specification

### Versions that support Unity

* 2019.4.0 or higher

## How to Use

1. using Gpm.Declares Cache Storage.
2. Most features are defined in GpmCacheStorage.
3. Request Cache using GpmCacheStorage.Request.

### Request
Request data from url through Request.
* Data is stored in cache and reused when invoking the same url.
* CacheRequestType lets you define when to validate to a server.
* If the data is the same when validating to the server, reuse the cache without receiving it again.

```cs
using Gpm.CacheStorage;

public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### GpmCacheResult
Result value of cached data. Returns cache information and data.
* IsSuccess allows you to obtain success or not.
* By default, data is stored as Data.
* Text or Json can be converted by encoding and the default is utf8.

```cs
* boolean IsSuccess() // Returns whether the result was successful or not.
* CacheInfoInfo; // Returns cache information.
* byte[] Data; // Returns cache data.
* Returns data encoded in string Text; // utf8.


* Returns data encoded in string GetTextData() // utf8.
* string GetTextData (EncodingEncoding) // Returns encoded data.

* T GetJsonData() // returns json data encoded in utf8.
* T GetJson Data (Encoding Encoding) // Return json data encoded in utf8.
```


```cs
public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (result) =>
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

### Texture caching request
Can request a texture cache using GpmCacheStorage.RequestTexture.
* If the texture is loaded after running the app, reuse them will be reused.
* Load and use cached textures when cached data and web data are the same data.

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

### CacheRequestType
Can decide when to re-validate cached data to the server.
The default is FIRSTPLAY You can make changes through SetCacheRequestType.

* ALWAYS
    * Validate that data has changed on the server at every request.
    * Same as GpmCacheStorage.RequestHttpCache.
* FIRSTPLAY
    * Verify to the server every time you make the first request after running the app.
    * Revalidates based on expiration or RequestTime settings.
* ONCE
    * Use cached data without validating to the server since the initial request.
    * Revalidates based on expiration or RequestTime settings.
* LOCAL
    * Uses cached data.
    * Same as GpmCacheStorage.RequestLocalCache.

```cs
public void Something()
{
    // whenever he requests to re-confirm adequacy of settings.
    CacheRequestType requestType = CacheRequestType.ALWAYS;
    GpmCacheStorage.SetCacheRequestType(requestType);
}
```

Can request and able to request.


```cs
using Gpm.CacheStorage;

public void Something()
{
    // Revalidate every time requested
    string url;
    CacheRequestType requestType = CacheRequestType.ALWAYS;
    GpmCacheStorage.Request(url, requestType, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### ReRequestTime
FIRSTPLAY, ONCE will reuse the cache until it expires based on the data received.
However, you can set the frequency of revalidation requests within the cluster.

The SetRequestTime setting allows you to set the request period in the cla.
* After a set number of seconds, the server will be re-validated upon callback.
* The default is 0.
* Do not re-request when set to 0.

```cs
public void Something()
{
    // Cache after 5 minutes of request is re-validated to the server
    double fiveMinutes = 5 * 60;
    GpmCacheStorage.SetReRequestTime(fiveMinutes);
}
```

Can request and a factor when request

```cs
using Gpm.CacheStorage;

public void Something()
{
    // Cache that has been requested for 5 minutes is revalidated to the server
    string url;
    double fiveMinutes = 5 * 60;
    GpmCacheStorage.Request(url, fiveMinutes, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```


### Cache Expiration
Calculates expiration based on the header received from the server and verifies it again.
* If the max-age of CacheControl is present, re-validate it after seconds of that value.
* If Expired has a header, request it again after that time.

### CacheControl Settings
* If CacheControl has noStore, disable the cache.
* Always revalidate if noCache is present in CacheControl.
* Same as CacheRequestType.ALWAYS setting or max-age 0


### Capacity control
Can adjust the cache capacity and number so that there are not too many caches.

#### SetMaxSize
Sets the maximum capacity.
```cs
public void Something()
{
    // Delete from unnecessary cache when cache capacity exceeds 10MB
    long maxSize = 10 * 1024 * 1024; // 10 MB
    boolean appplayStorage = true; // apply storage (automatic deletion)
    GpmCacheStorage.SetMaxSize(maxSize, applayStorage);
}
```

#### SetMaxCount
Can set the maximum number.
```cs
public void Something()
{
    // Delete from unnecessary cache when more than 50000 caches are exceeded
    int maxCount = 50000;
    boolean appplayStorage = true; // apply storage (automatic deletion)
    GpmCacheStorage.SetMaxCount(maxCount, applayStorage);
}
```

### SetUnusedPeriodTime
Caches that have not been used for that time period (seconds) are automatically deleted.
```cs
public void Something()
{
    // Delete cache that has not been used for 1 month
    double month = 24 * 60 * 60 * 30;
    GpmCacheStorage.SetUnusedPeriodTime(mont);
}
```

### SetRemoveCycle
Removes the cache of the destination to be removed every corresponding number of seconds.
If you delete many caches at once, it can be loaded and distributed.
```cs
public void Something()
{
    // Delete cache to be removed every 2
    double twoSeconds = 2;
    GpmCacheStorage.SetRemoveCycle(mont);
}
```

## API

### Request

Request data with url.
If cached data and web data are the same data, use cached data.

**API**
```cs
public static CacheInfo Request(string url, Action<GpmCacheResult> onResult)
```
```cs
public static CacheInfo Request(string url, CacheRequestType requestType, Action<GpmCacheResult> onResult)
```
```cs
public static CacheInfo Request(string url, double reRequestTime, Action<GpmCacheResult> onResult)
```
```cs
public static CacheInfo Request(string url, CacheRequestType requestType, double reRequestTime, Action<GpmCacheResult> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.Request(url, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```
```cs
public void Something()
{
    string url;
    GpmCacheStorage.Request(url, CacheRequestType.ALWAYS, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### RequestHttpCache

Request data by url.
If the cached data and the web data are the same data, the cached data is used.

**API**
```cs
public static CacheInfo RequestHttpCache(string url, Action<GpmCacheResult> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestHttpCache(url, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
        }
    });
}
```

### RequestLocalCache

Request already cached data by url.
Fails if not cached.

**API**
```cs
public static CacheInfo RequestLocalCache(string url, Action<GpmCacheResult> onResult)
```

**Example**
```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestLocalCache(url, (result) =>
    {
        if (result.IsSuccess() == true)
        {
            bytes[] data = result.Data;
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
public static double GetReRequestTime()
```

**Example**
```cs
public double GetReRequestTime()
{
    return GpmCacheStorage.GetReRequestTime();
}
```

### SetReRequestTime

Can set the webcache re-request time.
Default is 0. The unit is seconds.


**API**
```cs
public static void SetReRequestTime(long value)
```

**Example**
```cs
public void SetReRequestTime()
{
    double reRequestTime = 5 * 60;
    GpmCacheStorage.SetReRequestTime(reRequestTime);
}
```


### GetUnusedPeriodTime

Can know how long to delete unnecessary assets.

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

### SetUnusedPeriodTime

Sets the deletion period for unnecessary assets.
The default is 0. The unit is seconds.

**API**
```cs
public static void SetUnusedPeriodTime(double value)
```

**Example**
```cs
public void SetUnusedPeriodTime()
{
    double unUsedPeriodTime = 5 * 60 * 60;
    GpmCacheStorage.SetUnusedPeriodTime(unUsedPeriodTime);
}
```

### GetRemoveCycle
Can see the deletion of delay.

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

### SetRemoveCycle
Setting the deletion of delay.
The default value is 0.It was early units.

**API**
```cs
public static void SetRemoveCycle(double value)
```

**Example**
```cs
public void SetRemoveCycle()
{
    double reRequestTime = 5 * 60;
    GpmCacheStorage.SetRemoveCycle(reRequestTime);
}
```

### GetCacheRequestType

Can determine the CacheRequestType that is applied when requesting GpmCacheStorage.Request.

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

### SetCacheRequestType

Sets the CacheRequestType that is applied when requesting GpmCacheStorage.Request.

**API**
```cs
public static void SetCacheRequestType(CacheRequestType value)
```

**Example**
```cs
public void SetCacheRequestType()
{
    CacheRequestType reRequestTime = 5 * 60;
    GpmCacheStorage.SetCacheRequestType(reRequestTime);
}
```