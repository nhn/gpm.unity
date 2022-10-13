# Release notes

🌏 [한국어](ReleaseNotes.md)

## v1.0.1

### Date

* 2022.10.13

### Fixed
* Fixed local file read button connection invalid bug in sample
* Fixed a bug that did not format the last Mercury date when communicating with http

## v1.0.0

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

## v0.2.1

### Date

* 2022.07.08

### Updated
* Updated Common 2.1.0 to 2.1.2

## v0.2.0

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