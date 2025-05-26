# Release notes

🌏 [한국어](ReleaseNotes.md)

## 1.2.5

### Date

* 2025.5.20

### Updated

* Improved to ensure assetMap Window is properly initialized [(544)](https://github.com/nhn/gpm.unity/issues/544)

## 1.2.4

### Date

* 2024.12.19

### Fixed

* Fixed the issue where TerrainData dependency couldn't be found [(460)](https://github.com/nhn/gpm.unity/issues/460)
* Fixed the issue where some Scene data dependencies were ignored [(540)](https://github.com/nhn/gpm.unity/issues/540)
* Fixed the issue where an error occurred when searching for broken assets in resources [(541)](https://github.com/nhn/gpm.unity/issues/541)

## 1.2.3

### Date

* 2024.10.15

### Updated

* Removed Deprecated APIs by Unity version

### Fixed

* Fixed the freezing issue that occurs when using it with the Behavior Package
  [(538)](https://github.com/nhn/gpm.unity/issues/538)

## 1.2.2

### Date

* 2022.07.08

### Updated
* Updated Common 2.0.0 to 2.1.2

## 1.2.1

### Date

* 2021.3.02

### Fixed
* When removing all unnecessary assets and restoring them, modified so that only the checked assets are applicable.

## 1.2.0

### Date

* 2021.2.23

### Features

* Added the features to find and remove unnecessary assets
    * Optimize project size by removing unnecessary assets
    * Built-in, Assetbundle, Path filtering available

### Updated

* Performance improvement when progress ui is displayed
* Improved cache performance by excluding modeling dependency check

## 1.0.2

### Date

* 2021.2.03

### Updated

* Improved UI to show progress when ReferenceFind and IssuesCheck
 
### Fixed

* Fixed a problem with slow response when there were many issues in the project
* Fixed an error when asset properties were deleted in ReferenceFind
* Fixed a problem where seen as a compnent missing even when the referenced asset is a component

## 1.0.1

### Date

* 2021.1.19

### Fixed

* Fixed uistyle not visible in unity 2019 or higher

## 1.0.0

### Features

* Asset Map
* Asset Issue
* Asset Find
