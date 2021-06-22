# Profiler

🌏 [English](README.en.md)

## 🚩 목차

* [개요](#개요)
* [스펙](#스펙)
* [기능 설명](#기능-설명)
* [사용 방법](#사용-방법)
* [Release notes](./ReleaseNotes.md)

## 개요

* **Profiler**는 Unity에서 디바이스 성능과 시스템 정보를 화면에서 확인할 수 있어 최적화에 도움을 주는 툴입니다.

## 스펙

### Unity 지원 버전

* 2018.4.0 이상

## 기능 설명

### Performance Profiler
* 실시간 CPU와 GPU의 성능을 확인할 수 있습니다.

![performance_profiler](images/performance_profiler.gif)
1. FPS
    * FPS와 FrameTime을 보여줍니다.
2. AvgGroup
    * Avg 평균 FrameTime을 보여줍니다.
    * Min 최소 FrameTime을 보여줍니다.
    * Max 최대 FrameTime을 보여줍니다.
3. Script
    * 스크립트의 FrameTime을 보여줍니다.
4. Render
    * LastUpdate 이후 프레임이 렌더링이 끝날 때까지의 FrameTime을 보여줍니다.
5. Graph
    * Script와 Render의 FrameTime을 시각적으로 보여줍니다.

#### 원하는 옵션만 따로 확인할 수 있습니다.
![profiler_edit_performance](images/profiler_edit_performance.gif)
    

### Memory Profiler
* 실시간 메모리 할당과 사용량을 확인할 수 있습니다.

![memory_profiler](images/memory_profiler.gif)
1. reserved
    * OS에서 앱에 예약된 총메모리
2. allocated
    * OS에서 앱에 할당한 메모리
3. Gfx
    * Graphic Driver의 예상 메모리 사용량
    * Development 활성화 시 사용
4. GC Heap
    * script에서 할당된 힙 메모리
5. GC Used
    * script에서 사용 중인 메모리

#### 원하는 옵션만 따로 확인할 수 있습니다.
![profiler_edit_memory](images/profiler_edit_memory.gif)


### Rendering Profiler
* 렌더링에 사용되는 수치를 실시간으로 확인 가능합니다.
* Unity 2020.2 이상부터 사용 가능한 가능힙니다.

![render_profiler](images/render_profiler.png)

1. SetPass
    * 한 프레임을 렌더링할 때 호출한 셰이더 Pass의 수를 보여줍니다.
2. Draw Calls
    * 한 프레임을 렌더링할 때 호출한 DrawCall 수를 보여줍니다.
3. Total batch
    * 한 프레임을 렌더링할 때 호출한 총Batch 수를 보여줍니다.
4. Triangles
    * 한 프레임을 렌더링할 때 처리한 삼각형 수를 보여줍니다.
5. Vertices
    * 한 프레임을 렌더링할 때 처리한 정점  수를 보여줍니다.

#### 원하는 옵션만 따로 확인할 수 있습니다.
![profiler_edit_rendering](images/profiler_edit_rendering.gif)

### System Profiler
* 시스템 정보를 확인할 수 있습니다.

![system_profiler](images/system_profiler.png)

1. Os
    * 버전을 포함하여 장치의 OS에 대한 자세한 정보를 보여줍니다.
2. Device model
    * 디바이스의 모델명을 보여줍니다.
3. Processor type(CPU)
    * 프로세서 이름을 보여줍니다.
4. Processor count
    * 프로세서의 수를 보여줍니다.
5. Graphics device name(GPU)
    * 그래픽 카드 이름을 보여줍니다.
6. Graphics device vender
    * 그래픽 장치의 공급 업체를 보여줍니다.
7. Graphics device version
    * 그래픽 API 유형 및 드라이버 버전을 보여줍니다.

#### 원하는 옵션만 따로 확인할 수 있습니다.
![profiler_edit_system](images/profiler_edit_system.gif)
    

## 사용 방법

### 사용 준비하기

* GpmProfiler GameObject 설정    
    * **GPM/Profiler/Prefabs/GpmProfiler.prefab** 파일을 Scene에 추가합니다.

### 런타임에서  Profiler 편집하기

* 플랫폼별 편집 방법
    * 플랫폼 공통
        * **F5** Key로 편집 창을 활성화합니다.
    * iOS/Android 플랫폼은 제스처로 편집 창을 활성화합니다.
        * 손가락 네 개로 2초간 화면을 터치합니다.

* 편집창 활성화 이후
    * 활성화 상태에서 드래그하면 원하는 위치로 이동합니다.
    * 원하는 옵션만 따로 확인할 수 있습니다.
    ![profiler_edit_main](images/profiler_edit_main.gif)