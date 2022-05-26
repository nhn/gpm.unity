# WebCacheImage

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [사용 방법](#사용-방법)
* [API](#api)

## 개요

URL을 이용하여 웹 이미지를 캐시하여 이미지를 보여주는 컴포넌트 입니다.

## 사용 방법
UI 오브젝트에 **WebCacheImage** 컴포넌트를 추가합니다. 
* RawImage가 없다면 RawImage컴포넌트도 같이 생성됩니다.
* RawImage가 있다면 RawImage컴포넌트에 연동됩니다.

![WebCacheImage.png](https://github.com/nhn/gpm.unity/blob/main/docs/UI/WebCacheImage/images/WebCacheImage.png?raw=true)

1. 이미지를 불러올 URL입니다.
2. 웹 요청을 통해 이미지를 얻을 경우 딜레이가 있습니다. 캐시가 있을경우 미리 불러옵니다.
3. Texture가 요청을 통해 Load되었을떄의 이벤트 입니다.

## API

### SetUrl

이미지를 불러올 URL을 설정합니다.

**Example**
```cs
WebCacheImage cache;

cache.SetUrl(cacheData.url);
```

### SetLoadTextureEvent

이미지를 로드할 때 이벤트를 설정합니다.

**Example**
```cs
WebCacheImage cache;
cache.SetLoadTextureEvent(OnLoadTexture);

public void OnLoadTexture(Texture texture)
{
}
```