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

**Example**
```cs
string url;
GpmCacheStorage.RequestHttpCache(url, (result) =>
{
	if (result.success == true)
	{
		bytes[] data = result.data;
	}
});
```

### RequestLocalCache

Request already cached data by url.
Fails if not cached.

**Example**
```cs
string url;
GpmCacheStorage.RequestLocalCache(url, (result) =>
{
	if (result.success == true)
	{
		bytes[] data = result.data;
	}
});
```

### GetCachedTexture

Request an already cached texture by url.
If the texture is loaded after running the app, it will be reused.

**Example**
```cs
string url;
cacheInfo = GpmCacheStorage.GetCachedTexture(url, (cachedTexture) =>
{
	if (cachedTexture != null)
	{
		Image.texture = cachedTexture.texture;
	}
});
```


### RequestTexture

Request cached data by url.
If the texture is loaded after running the app, it will be reused.
If the cached data and web data are the same data, the cached texture is loaded and used.

**Example**
```cs
string url;
cacheInfo = GpmCacheStorage.RequestTexture(url, (cachedTexture) =>
{
	if (cachedTexture != null)
	{
		Image.texture = cachedTexture.texture;
	}
});
```

### GetCacheCount

Can see the number of caches used.

**Example**
```cs
GpmCacheStorage.GetCacheCount();
```

### GetCacheSize
Can see the amount of cache used.

**Example**
```cs
GpmCacheStorage.GetCacheSize();
```

### ClearCache

Remove the managed cache.

**Example**
```cs
GpmCacheStorage.ClearCache();
```

### SetCachePath

Sets the path to the managed cache.
The default is Application.temporaryCachePath .

**Example**
```cs
string path = Application.temporaryCachePath;
GpmCacheStorage.SetCachePath(path);
```

### GetCachePath

Can know the path to the managed cache.

**Example**
```cs
GpmCacheStorage.GetCachePath();
```