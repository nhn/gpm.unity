# Duplicate Library Search Tool(DLST)

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [스펙](#스펙)
* [검색 규칙](#검색-규칙)
* [사용방법](#-사용방법)

## 개요

* 많은 외부 라이브러리들을 사용할 경우, 라이브러리 중복 문제가 발생할 수 있습니다.
* DLST는 중복되는 라이브러리들을 검색해서 지울 수 있는 툴입니다.

## 스펙

### Unity 지원 버전

* 2018.4.0 이상

### 지원하는 라이브러리 형식

* jar
* aar
* dll
* framework
* bundle

## 검색 규칙

### 검색 폴더

* \*/Plugins/*

### 이름 규칙

DLST에서는 라이브러리 파일 이름을 다음과 같이 구분합니다.
```
{filename}.{extension}
{filename}-{version}.{extension}
{filename}_{version}.{extension}
{filename} {version}.{extension}
```

검색 시에는 version을 제외하고 비교를 합니다.</br>
버전은 다음과 같은 형식으로 인식합니다.
```
정규식 : [a-zA-Z]?(\d+)(.\d+)?(.\d+)?(.\d+))

* 예 : 1.0 / 1.0.0 / 1.0.0.0 / v1.0.0 / r1.2 / a2.3.4
```

* 파일 이름 변환 예
    ```
    aaa-1.0.0.jar -> aaa.jar
    bbb-2.2.2.aar -> bbb.aar
    ccc-1.aar -> ccc-1.aar
    ddd-v1.aar -> ddd-v1.aar
    ddd-v1.0.0.aar -> ddd.aar
    eee-vvv.aar -> eee-vvv.aar
    ```

* 검색 예
    * 중복 라이브러리로 판단합니다.
        ```
        aaa-1.0.0.jar -> aaa.jar
        aaa-2.0.0.jar -> aaa.jar
        aaa-v3.0.0.jar -> aaa.jar
        ```
    * 중복 라이브러리로 판단하지 않습니다.
        ```
        bbb-2.2.2.aar -> bbb.aar
        bbbb-2.2.2.aar -> bbbb.aar
        bbb-ccc.aar -> bbb-ccc.aar
        ```

### 검색 옵션

* 라이브러리 이름에서 특정 문자열 무시
    * 검색 시 파일명에서 특정 문자열을 무시할 수 있습니다.
        ```
        * 설정 예
            파일명 : com.android.support.support-v4-25.3.1.aar
            무시할 문자열 : com.android.support.
            무시할 문자열 적용 후 파일명 : support-v4-25.3.1.aar
            검색 시 version, 확장자 제외 후 파일명 : support-v4

        * 검색 예
            무시할 문자열 : com.android.support.
            파일 1
                com.android.support.support-v4-25.3.1.aar
                -> 검색 시 파일명 : support-v4
            파일 2
                support-v4-27.0.0.aar
                -> 검색 시 파일명 : support-v4
            - 검색 결과 중복 라이브러리로 판단
        ```
* 검색에서 제외할 라이브러리 이름
    * 검색 시 설정된 이름과 같을 경우 검색 대상에서 제외합니다.
        ```
        * 설정 예 1

        제외할 라이브러리 이름 : play-services-auth

        파일명
            play-services-auth-15.0.1.aar
            -> 검색 시 파일명 : play-services-auth

        - 검색 대상에서 제외

        파일명
            com.google.android.gms.play-services-auth-15.0.1.aar 
            -> 검색 시 파일명 : com.google.android.gms.play-services-auth

        - 검색 대상에 포함
        ```
        ```
        * 설정 예 2

        무시할 문자열 : com.google.android.gms.
        제외할 라이브러리 이름 : play-services-auth

        파일명
            com.google.android.gms.play-services-auth-15.0.1.aar 
            -> 검색 시 파일명 : play-services-auth

        - 검색 대상에서 제외
        ```

## 🔨 사용방법

### DLST 실행

Menu > Tools > GPM > Duplicate Library Search Tool(DLST)

### UI

#### DLST 창

![DLST.png](images/DLST_Window.png)

1. '라이브러리 이름에서 무시할 문자열' 설정
2. '검색에서 제외할 라이브러리 이름' 설정
3. 중복 라이브러리 목록
    * 중복된 라이브러리를 표시합니다.
    * '새로 고침' : 검색 결과를 갱신합니다.
    * '삭제' : 라이브러리 목록에서 선택한 라이브러리를 삭제합니다.
4. 툴의 언어를 변경합니다. 지원 언어는 한국어, 영어입니다.

#### '라이브러리 이름에서 무시할 문자열' 설정 창

![String.png](images/DLST_String.png)

1. 설정된 문자열이 저장될 파일 위치를 지정합니다.
2. 문자열 목록
    * 설정된 문자열을 보여줍니다.
    * '추가' : 추가할 문자열을 입력합니다. 활성화된 버튼을 클릭하면 문자열이 목록에 추가됩니다.
    * '삭제' : 문자열 목록에서 선택한 문자열을 삭제합니다.

#### '검색에서 제외할 라이브러리 이름' 설정 창
	
![Library.png](images/DLST_Library.png)

1. 설정된 라이브러리 이름이 저장될 파일 위치를 지정합니다.
2. 라이브러리 이름 목록
    * 설정된 라이브러리 이름을 보여줍니다.
    * '추가' : 추가할 라이브러리 이름을 입력합니다. 활성화된 버튼을 클릭하면 라이브러리가 목록에 추가됩니다.
    * '삭제' : 라이브러리 이름 목록에서 선택한 라이브러리를 삭제합니다.