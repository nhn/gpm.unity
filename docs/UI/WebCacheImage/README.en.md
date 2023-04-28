# WebCacheImage

🌏 [한국어](README.md)

## 🚩 Table of Contents

* [Overview](#Overview)
* [How to use](#How-to-use)
* [API](#api)

## Overview

This component displays images by caching web images using URLs.

## How to use
Add a **WebCacheImage** component to your UI object.

* If RawImage does not exist, a RawImage component is also created.
* If there is a RawImage, it is linked to the RawImage component.

![WebCacheImage.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/WebCacheImage/images/WebCacheImage.png?raw=true)

1. This is the URL to load the image.
2. There is a delay when getting images via web request. If there is a cache, it is loaded in advance.
3. This event is when the Texture is loaded through a request.

## API

### SetUrl

Set the URL to load the image.

**Example**
```cs
WebCacheImage cache;

cache.SetUrl(cacheData.url);
```

### SetLoadTextureEvent

Set an event when loading an image.

**Example**
```cs
WebCacheImage cache;
cache.SetLoadTextureEvent(OnLoadTexture);

public void OnLoadTexture(Texture texture)
{
}
```