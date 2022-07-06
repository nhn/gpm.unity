# Release notes

🌏 [English](ReleaseNotes.en.md)

## 2.1.2

### Date

* 2022.07.06

### Update

* 내부 로직 개선

## 2.1.1

### Date

* 2022.06.07

### Update
* 임포트 할 때 기본적으로 overwrite 적용되도록 개선

## 2.1.0

### Date

* 2022.05.30

### Added
* 네트워크, 코루틴 관리 기능 추가

## 2.0.9

### Date

* 2022.03.10

### Updated
* FileStream Access 권한 명시적으로 개선 [(#184)](https://github.com/nhn/gpm.unity/issues/184)

## 2.0.8

### Date

* 2021.12.17

### Fixed
* 빌드 할때 warning 나오는 문제 수정
* 코루틴 오브젝트 변수 오타 수정

## 2.0.7

### Date

* 2021.12.13

### Added
* json Single 타입 지원 추가

### Changed
* multiLanguage Loader 확장 가능하도록 수정
* indicator 로직 개선

## 2.0.6

### Date

* 2021.09.01

### Fixed

* Unity bulit-in component와 같은 이름의 스크립트 파일명 수정

## 2.0.5

### Date

* 2021.08.30

### Fixed

* 유니티 패키지 임포트 실패 이슈 수정
* .net runtime 4.0 이하 대응

## 2.0.4

### Date

* 2021.07.05

### Fixed

* Unity 2020.2버전에서 컴파일 오류 수정

---

## 2.0.3

### Date

* 2021.07.05

### Fixed

* UnityWebRequest isNetworkError API가 Unity2020.2이후로 Deprecated 되어 수정

---

## 2.0.2

### Date

* 2021.05.17

### Changed

* 내부 지표 변경

---

## 2.0.1

### Date

* 2021.03.03

### Added

* Assembly definition

---

## 2.0.0

### Date

* 2020.12.21

### Updated

* TOAST Kit에서 Game Package Manager로 브랜드 이름 변경

---

## 1.0.1

### Date

* 2020.08.21

### Added

* Compress 모듈 추가
* Multilanguage - 시스템 언어 가져오기 API 추가

### Updated

* Unity 최소 지원 버전 2018.4.0으로 상향
* SharpZipLib.dll 제거
* Multilanguage - 해당 시스템 언어를 지원할 경우 시스템 언어를 보여주도록 설정

---

## 1.0.0

### Features

* Multilanguage
* Indicator
* Log
* JSON parser