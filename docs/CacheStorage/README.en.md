# CacheStorage

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#overview)
* [Installation](#installation)
* [Specification](#specification)
* [API](#api)
* [Release notes](./ReleaseNotes.en.md)

## Overview

* CacheStorage supports Cache when web communications are performed in Unity.
* Cache can be used to improve performance by reusing the data received when communicating.

### Performance Improvements

Store and reuse content based on HTTP when communicating on a network.
If the content is not modified, the response does not include the content, which significantly improves performance.

![](Images/1_en.png)

* CacheStorage sample-based performance test
    * UnityWebrequest: 28ms
    * WebCache: 14ms
    * Local: 1ms 

When you use the web cache, Can see that it is about twice as fast as normal communication.

### Ease of Use
It is simple as the management point is unified with one URL.

Reusing content is very fast. At the same time, data management of up-to-date content is also required.
If you use the web cache, it is easy to verify that the content is up-to-date with the same URL and can be reused.

### Capacity management
Can control the capacity by managing the cache.

![](Images/CacheStorage_logic_en.png)

1. Runtime Management
* It removes content that has not been used for a long time in real time.
* Both UnusedPeriodTime and RemoveCycle must be set to operate.
    * UnusedPeriodTime
        * Clears caches that have not been used for a set number of seconds.
    * RemoveCycle
        * Caches being removed are removed one by one every set number of seconds so that performance is not affected.

2.  Conditional Management
* When receiving new content, it is removed so that it does not exceed the set capacity and number.
* Removes caches with lower priority.
    * MaxSize
        * If the number of managed caches exceeds the set number, the ones with the lowest priority are deleted.
    * MaxCount
        * If the managed cache exceeds the set capacity, the lower priority is deleted first.

## Installation

1. [Install Game Package Manger](https://assetstore.unity.com/packages/tools/utilities/game-package-manager-147711)
2. Run : [Unity Menu > Tools > GPM > Manager](https://github.com/nhn/gpm.unity/blob/main/README.en.md#execute)
3. Service installation : CacheStorage

## Specification

### Versions that support Unity

* 2019.4.0 or higher

## How to Use

1. using Gpm.Declares Cache Storage.
2. Most features are defined in GpmCacheStorage.
3. Initialize it using GpmCacheStorage.Initialize.
3. Request Cache using GpmCacheStorage.Request.

### NameSpace
```cs
using Gpm.CacheStorage;
```

### Initialize
To use CacheStorage, it must be initialized.
* Calls GpmCacheStorage.Initialize.

Sets the parameters to be used for CacheStorage.

* maxCount
    * If the set maximum number is exceeded, caches with lower priority are deleted.
    * Unlimited when set to 0.
* maxSize
    * If the set maximum capacity is exceeded, caches with lower priority are erased.
    * Unlimited when set to 0.
* reRequestTime
    * Cache that has passed the set time (seconds) at the time of request is re-validated.
    * When set to 0, revalidation is not performed based on request time.

* defaultRequestType
    * Re-validates based on the type set at the time of request.
        * ALWAYS
            * Revalidate that data has changed on the server at every request.
        * FIRSTPLAY
            * It is revalidated every time the app is restarted, and it is also revalidated when the validity period is over.
        * Once
            * It is reused and revalidated when the expiration date is over.
        * LOCAL
            * Use stored cache.
* unusedPeriodTime
    * Clear caches that have not been used for the set amount of time (seconds).
    * When unusedPeriodTime or removeCycle is set to 0, real-time removal is not performed.
* removeCycle
    * Remove caches that are removed one by one every set number of seconds so that performance is not affected.
    * When unusedPeriodTime or removeCycle is set to 0, real-time removal is not performed.

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
Request data from url through Request.
* Data is stored in cache and reused when invoking the same url.
* CacheRequestType lets you define when to validate to a server.
* If the data is the same when validating to the server, reuse the cache without receiving it again.

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
Result value of cached data. Returns cache information and data.
* IsSuccess allows you to obtain success or not.
* By default, data is stored as Data.
* Text or Json can be converted by encoding and the default is utf8.

```cs
boolean IsSuccess() // Returns whether the result was successful or not.
CacheInfoInfo; // Returns cache information.
byte[] Data; // Returns cache data.
string Text; // Returns the utf8 encoded data.

string GetTextData() // Returns the utf8 encoded data.
string GetTextData(Encoding encoding) // Returns encoded data.

T GetJsonData<T>() // returns json data encoded in utf8.
T GetJsonData<T>(Encoding encoding) // Return json data encoded in utf8.
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
The return value when requesting the cache. You can get the cache request status.

```cs
bool keepWaiting() // Returns whether to wait in coroutine.
void Cancel() // Cancel the request. Callbacks are not dispatched for canceled requests.
```

#### Wait for coroutine
Can wait in a coroutine using CacheRequestOperation.
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

#### Cancel request
Can opt out of receiving callbacks by canceling the request.
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

### Texture caching request
Can request a texture cache using GpmCacheStorage.RequestTexture.
* If the texture is loaded after running the app, reuse them will be reused.
* Load and use cached textures when cached data and web data are the same data.

```cs
public void Something()
{
    string url;
    GpmCacheStorage.RequestTexture(url, (cachedTexture) =>
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
The result of the cached texture. Return cache information.
* Can get cached textures.
* Can know whether the texture has changed through updateData.

```cs
CacheInfo info // Returns cache information.
Texture2D texture; // Return the resulting texture.
bool requested;  // When true, this is a new request from the web.
bool updateData;  // When true, this is the newly updated texture.

void DestroyTexture() // Destroys the texture and excludes it from managed textures as well.
void ReleaseCache() // Remove from managed texture. It doesn't destroy textures.
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

## More effective web cache
Web cache is about twice as fast as normal requests.
Importing locally is faster, but cannot determine if it is up to date.

![](Images/3_en.png)

Can use the web cache more effectively by validating it only when you need it.

### Web Cache Validation Strategy

If security is critical or requires continuous renewal, use normal network communications to ensure integrity.
In addition, different verification strategies depending on whether content is more important for performance or integrity can further improve performance.

![](Images/4_en.png)

Cache Storage supports 4 validation strategies

### CacheRequestType
Can decide when to re-validate cached data to the server.
More revalidation ensures integrity, and more reuse improves performance.

* ALWAYS
    * Revalidate that data has changed on the server at every request.
    * Same as GpmCacheStorage.RequestHttpCache.
* FIRSTPLAY
    * Re-validated every time the app is re-launched, and also re-verified when the validity period is over.
    * Revalidates based on expiration or RequestTime settings.
* ONCE
    * Will be re-verified at the end of the validity period.
    * Revalidates based on expiration or RequestTime settings.
* LOCAL
    * Uses cached data.
    * Same as GpmCacheStorage.RequestLocalCache.

#### Can request and able to request
* If no argument is used, the default value set in Initialize is used.

```cs
using Gpm.CacheStorage;

public void Something()
{
    // Revalidate every time requested
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
FIRSTPLAY, ONCE will reuse the cache until it expires based on the data received.
However, you can set the frequency of revalidation requests within the cluster.
* After a set number of seconds, the server will be re-validated upon callback.
* Do not re-request when set to 0.

#### Can request and a factor when request
* If the argument is 0 or not used, the default value set in Initialize is used.

```cs
using Gpm.CacheStorage;

public void Something()
{
    // Cache that has been requested for 5 minutes is revalidated to the server
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

### Viewer
Can view cache information for Cache Storage.

* How to use
    * Can be opened through GPM/CacheStorage/Viewer in the menu.

![](Images/viewer.png)

### 1. Management
This is the Managed Cache menu.

* Size: Current cache capacity / maximum capacity (byte unit)
    * The current cache capacity and the set maximum capacity.
    * Keeps the maximum capacity not exceeded.
* Count: Current cache count / maximum count
    * The current cache number and the set maximum number.
    * Keeps the maximum number not exceeded.

### 2. Request Info
This information is used when requesting cache.

* Default RequestType
    * Re-validates based on the type set at the time of request.
        * ALWAYS
            * Revalidate that data has changed on the server at every request.
        * FIRSTPLAY
            * It is revalidated every time the app is restarted, and it is also revalidated when the validity period is over.
        * Once
            * It is reused and revalidated when the expiration date is over.
        * LOCAL
            * Use stored cache.
* ReRequest
    * Cache that has passed the set time (seconds) at the time of request is re-validated.
    * When set to 0, revalidation is not performed based on request time.

### 3. Auto Remove
It removes content that has not been used for a long time in real time.
Both UnusedPeriodTime and RemoveCycle must be set for this to work.

* UnusedPeriodTime
    * Clear caches that have not been used for the set amount of time (seconds).
    * Do not remove real-time when unusedPeriodTime or removeCycle is 0.
* RemoveCycle
    * Remove caches that are removed one by one every set number of seconds so that performance is not affected.
    * Do not remove real-time when unusedPeriodTime or removeCycle is 0.

### 4. Cache data list
This is a list of managed cache data.

* Name: Cache name
* Url: cache path
* Size : Cache size (byte unit)
* Exfires: Remaining time until expiration date
* Remain: Remaining time until cache validation
    * Re-verification after the remaining time has elapsed.
    * The shorter of the remaining time until the expiration date and the ReRequest time (in seconds)
* Remove: Remaining time until removal
    * If not used for the remaining time, it will be removed.
    * Time Used / Time set as UnusedPeriodTime (in seconds)
    * Do not remove real-time when unusedPeriodTime or removeCycle is 0.

### 5. Cache Details Info
Cache data details selected from the list.

## API

### Initialize
To use CacheStorage, it must be initialized.

* maxCount
    * If the set maximum number is exceeded, caches with lower priority are deleted.
    * Unlimited when set to 0.
* maxSize
    * If the set maximum capacity is exceeded, caches with lower priority are erased.
    * Unlimited when set to 0.
* reRequestTime
    * Cache that has passed the set time (seconds) at the time of request is re-validated.
    * When set to 0, revalidation is not performed based on request time.
* defaultRequestType
    * Re-validates based on the type set at the time of request.
        * ALWAYS
            * Revalidate that data has changed on the server at every request.
        * FIRSTPLAY
            * It is revalidated every time the app is restarted, and it is also revalidated when the validity period is over.
        * Once
            * It is reused and revalidated when the expiration date is over.
        * LOCAL
            * Use stored cache.
* unusedPeriodTime
    * Clear caches that have not been used for the set amount of time (seconds).
    * When unusedPeriodTime or removeCycle is set to 0, real-time removal is not performed.
* removeCycle
    * Remove caches that are removed one by one every set number of seconds so that performance is not affected.
    * When unusedPeriodTime or removeCycle is set to 0, real-time removal is not performed.
    
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

Request data with url.
If cached data and web data are the same data, use cached data.

* url
    * Cache url to request.
* requestType
    * The type of data that determines when cached data should be re-validated to the server.
    * If no ruler is used, the default value set by Initialize is used.
* reRequestTime
    * Can set the frequency of re-verification requests on a per-function basis.
    * After the set time (in seconds) has elapsed since the last verification, it will be verified again.
    * If the argument is 0 or not used, the default value set in Initialize is used.

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
Result value of cached data. Returns cache information and data.
* IsSuccess allows you to obtain success or not.
* By default, data is stored as Data.
* Text or Json can be converted by encoding and the default is utf8.

**API**
```cs
boolean IsSuccess() // Returns whether the result was successful or not.
CacheInfoInfo; // Returns cache information.
byte[] Data; // Returns cache data.
string Text; // Returns the utf8 encoded data.

string GetTextData() // Returns the utf8 encoded data.
string GetTextData(Encoding encoding) // Returns encoded data.

T GetJsonData<T>() // returns json data encoded in utf8.
T GetJsonData<T>(Encoding encoding) // Return json data encoded in utf8.
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
The return value when requesting the cache. You can get the cache request status.
* You can await in a coroutine.
* You can also cancel cache requests.

**API**
```cs
bool keepWaiting() // Returns whether to wait in coroutine.
void Cancel() // Cancel the request. Callbacks are not dispatched for canceled requests.
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

Request data by url.
If the cached data and the web data are the same data, the cached data is used.

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

Request already cached data by url.
Fails if not cached.

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

Request an already cached texture by url.
If the texture is loaded after running the app, it will be reused.

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

Request cached data by url.
If the texture is loaded after running the app, it will be reused.
If the cached data and web data are the same data, the cached texture is loaded and used.

* url
    * Cache url to request.
* requestType
    * The type of data that determines when cached data should be re-validated to the server.
    * If no ruler is used, the default value set by Initialize is used.
* reRequestTime
    * Can set the frequency of re-verification requests on a per-function basis.
    * After the set time (in seconds) has elapsed since the last verification, it will be verified again.
    * If the argument is 0 or not used, the default value set in Initialize is used.
* preLoad
    * Read pre-stored cache before verifying on the web.
    * The callback is called again if the content has changed since validation.

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

The result of the cached texture. Return cache information.
* Can get cached textures.
* Can know whether the texture has changed through updateData.

**API**
```cs
CacheInfo info // Returns cache information.
Texture2D texture; // Return the resulting texture.
bool requested;  // When true, this is a new request from the web.
bool updateData;  // When true, this is the newly updated texture.

void DestroyTexture() // Destroys the texture and excludes it from managed textures as well.
void ReleaseCache() // Remove from managed texture. It doesn't destroy textures.
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

Can see the amount of cache used.

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

### ClearCache

Remove the managed all cache.

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

Remove the managed cache.

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