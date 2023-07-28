# Release notes

🌏 [한국어](ReleaseNotes.md)

## 1.3.1

### Date

* 2023.07.31

### Fixed
* Fixed deprecation warning[(414)](https://github.com/nhn/gpm.unity/issues/414)

## 1.3.0

### Date

* 2023.05.24

### Added
* Added cache clear function
   * RemoveCache
* Added texture disconnection and texture destruction functions in ManagedTexture
   * DestroyTexture, ReleaseCache
* Added ability to cancel during request and to wait in coroutine
   * CacheRequestOperation
* Added the ability to view local time in Viewer

### Updated
* Optimized date calculation

### Fixed
* Fixed a waiting problem when requesting a request that is already being requested as Local
* Improved so that the texture managed when requesting RequestTexture can be read even if it is destroyed externally

## 1.2.0

### Date

* 2023.04.24

### Add
* Add initialization function GpmCacheStorage.Initialize
    * Modified to work only when explicitly initialized

### Updated
* Updated Common 2.3.0
* Improved synchronization performance for local cache file management
* Changed internal file format for cache management
    * json -> MessagePack

### Fixed
* Fixed a problem that the previous callback was not cleared when an exception occurred in the callback
* Fixed exception when loading non-cached files

## 1.1.2

### Date

* 2023.03.15

### Updated
* Removed SetCachePath function

### Fixed
* Fixed folder Access Denied issue when updating on iOS

## 1.1.1

### Date

* 2023.03.10

### Fixed

* Fixed a problem that all request callbacks are called regardless of the url when a request is received

## 1.1.0

### Date

* 2023.03.10

### Added
* Added CacheStorage viewer tool
* Added function to put RequestTexture RequestType
* Add RequestTexture preload

### Updated
* Improved to update expiration date information even when NotModified code occurs
* maxCount default set to 10000
* maxSize default set to 256MB
* Improved to maintain the same data internally even when receiving cache again

### Fixed
* Fixed a bug that could not be read when the LastModified value was 0
* Fixed an incorrect calculation when setting the ReRequest time
* Fixed an issue where capacity was calculated incorrectly when receiving a new cache
* Fixed access permission problem due to folder change in ios
* Fixed to receive callback when requesting at the same time
* Fixed to work normally even if StringToValue is null
* Fixed to calculate caches that are being automatically deleted when deleting due to size restrictions

## 1.0.1

### Date

* 2022.10.13

### Fixed
* Fixed local file read button connection invalid bug in sample
* Fixed a bug that did not format the last Mercury date when communicating with http

## 1.0.0

### Date

* 2022.08.26

### Added
* Support for automatic background deletion according to the caching validity period
* Support CacheControl function
* CacheResult text, json conversion function added
* Request type added when the set re-request time has not expired
    * ALWAYS: Validate that data changes to the server at every request
    * FIRSTPLAY: Validate to server at first request after app launch
    * ONCE: Use cached data without verification to the server since the initial request
    * LOCAL: Uses cached data.

### Updated
* Raise the minimum version to 2019.4 according to the 1.3.a Versions of Unity contents of the Unity Guidelines.
    * Link : [Unity Guidelines](https://assetstore.unity.com/publishing/submission-guidelines)
* Common v2.2.2 update
* Cache calculation optimization
* Optimize import data
* Change based on re-request time (Tick -> Seconds)

## 0.2.1

### Date

* 2022.07.08

### Updated
* Updated Common 2.1.0 to 2.1.2

## 0.2.0

### Date

* 2022.06.28

### Added
* Added maximum capacity setting function
* Added maximum number setting function
* Added web cache re-request period setting function
* Added cache eviction priority sort
    1. Expired
    2. It has been 1 month since access
    3. It has been 1 week since access
    4. Created file index
* Add Sample
* Add API
    * SetMaxCount, GetMaxCount
    * SetMaxSize, GetMaxSize
    * SetReRequestTime, GetReRequestTime

## 0.1.0

### Date

* 2022.05.30

### Features

* Http Cache
* Local Cache
* CachedTexture