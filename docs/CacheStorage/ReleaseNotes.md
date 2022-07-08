# Release notes

🌏 [English](ReleaseNotes.en.md)

## v0.2.1

### Date

* 2022.07.08

### Updated
* Common 2.1.0을 2.1.2로 업데이트

## v0.2.0

### Date

* 2022.06.28

### Added
* 최대 용량 설정 기능 추가
* 최대 개수 설정 기능 추가
* 웹 캐시 재요청 주기 설정 기능 추가
* 캐시 제거 우선순위 정렬 추가
    1. 만료된 것
    2. 접근한지 1달 지난 것
    3. 접근한지 1주 지난 것
    4. 생성된 파일 index
* 샘플 추가
* API 추가
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