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

url로 데이타를 요청합니다.
캐시된 데이타와 웹 데이타가 동일한 데이타인 경우 캐시 된 데이타를 사용합니다.

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

url로 이미 캐시 된 데이타를 요청합니다. 
캐시 되어있지 않은 경우 실패합니다.

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

url로 이미 캐시 된 텍스쳐를 요청합니다.
앱 실행 후 로드한 텍스쳐라면 재사용합니다.

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

url로 캐시 된 데이타를 요청합니다. 
앱 실행 후 로드한 텍스쳐라면 재사용합니다.
캐시 된 데이타와 웹 데이타가 동일한 데이타인 경우 캐시 된 텍스쳐를 로드하여 사용합니다.

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

관리 중인 캐시 수를 알 수 있습니다.

**Example**
```cs
GpmCacheStorage.GetCacheCount();
```

### GetCacheSize

관리 중인 캐시 용량을 알 수 있습니다.

**Example**
```cs
GpmCacheStorage.GetCacheSize();
```

### ClearCache

관리 중인 캐시를 제거합니다.

**Example**
```cs
GpmCacheStorage.ClearCache();
```

### SetCachePath

관리되는 캐시의 경로를 설정합니다.
기본은 Application.temporaryCachePath입니다.

**Example**
```cs
string path = Application.temporaryCachePath;
GpmCacheStorage.SetCachePath(path);
```

### GetCachePath

관리되는 캐시의 경로를 알 수 있습니다.

**Example**
```cs
GpmCacheStorage.GetCachePath();
```