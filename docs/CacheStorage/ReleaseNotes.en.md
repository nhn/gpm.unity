# Release notes

🌏 [한국어](ReleaseNotes.md)

## v1.0.0

### Date

* 2022.08.25

### Added
* Support for automatic background deletion according to the caching validity period
* Support CacheControl function
* CacheResult text, json conversion function added
* Request type added when the set re-request time has not expired
    * ALWAYS: Continuously check the cache on the server
    * FIRSTPLAY : Request cache check to the server only once during execution
    * ONCE: use local data after one request
    * LOCAL : Use only local data

### Updated
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