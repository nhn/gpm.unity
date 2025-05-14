# Release notes

🌏 [English](ReleaseNotes.en.md)

## 1.2.5

### Date

* 2025.5.14
* 
### Updated

* assetMap Window 초기화가 보장되도록 개선 [(544)](https://github.com/nhn/gpm.unity/issues/544)

## 1.2.4

### Date

* 2024.12.19

### Fixed

* TerrainData 의존성 못 찾는 문제 수정 [(460)](https://github.com/nhn/gpm.unity/issues/460)
* Scene 일부 데이터 의존성 무시되는 문제 수정 [(540)](https://github.com/nhn/gpm.unity/issues/540)
* 리소스 끊어진 에셋을 찾을 때 오류가 발생하는 부분 수정 [(541)](https://github.com/nhn/gpm.unity/issues/541)

## 1.2.3

### Date

* 2024.10.15

### Updated

* 유니티 버전별 Deprecated API 대응

### Fixed

* Behavior Package와 함께 사용 시 발생하는 프리징 문제 수정 [(538)](https://github.com/nhn/gpm.unity/issues/538)

## 1.2.2

### Date

* 2022.07.08

### Updated
* Common 2.0.0에서 2.1.2로 업데이트

## 1.2.1

### Date

* 2021.3.02

### Fixed
* 불필요한 에셋 전체 삭제 및 전체 복구시 체크된 에셋만 해당되도록 수정

## 1.2.0

### Date

* 2021.2.23

### Features

* 불필요한 에셋 찾고 제거하는 기능 추가
    * 미사용에셋을 제거하여 프로젝트 사이즈 최적화
    * Built-in, Assetbundle, path 필터링 가능

### Updated

* 진행도 ui 표기될때 성능 향상
* 모델링 의존성 체크 제외로 캐시 성능 향상
 
## 1.0.2

### Date

* 2021.2.03

### Updated

* 에셋 찾기, 이슈 검색할때 진행도 나오도록 UI개선
 
### Fixed

* 프로젝트에 issue 많을때 에디터 응답 느려지는 문제 수정
* 찾은 에셋의 속성이 사라질때 오류나는 문제 수정
* 참조되는 에셋이 컴포넌트일때도 컴포넌트 missing으로 나오던 문제 수정

## 1.0.1

### Date

* 2021.1.19

### Fixed

* 2019 이상 버전에서 보이지 않는 uiStyle 수정

## 1.0.0

### Features

* Asset Map
* Asset Issue
* Asset Find
