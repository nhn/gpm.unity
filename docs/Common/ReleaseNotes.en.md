# Release notes

🌏 [한국어](ReleaseNotes.md)

## 2.4.0

### Date

* 2024.05.17

### Fixed
* Improved internal logic.

## 2.3.3

### Date

* 2024.03.29

### Fixed
* Fixed compilation errors in .Net 2.1 environment


## 2.3.2

### Date

* 2024.03.29

### Updated
* Response to Apple Privacy Policy [(Apple Privacy Policy)](https://developer.apple.com/news/?id=3d8a9yyh)

## 2.3.1

### Date

* 2023.05.08

### Fixed
* Fixed MessagePack compilation error in .net21 .net4 environment[(#388)](https://github.com/nhn/gpm.unity/issues/388)

## 2.3.0

### Date

* 2023.04.24

### Added
* Added GPMLogger Exception Log
* Added MessagePack

### Updated
* Optimize internal network logic

## 2.2.3

### Date

* 2022.12.27

### Updated
* Internal domain change

## 2.2.2

### Date

* 2022.08.26

### Updated
* Modified to include both property get set in thirdparty Json must be readable
* Fields are now added when using the SerializeField attribute in a thirdparty Json.
* Fields are now ignored when using the JsonSkip attribute in a thirdparty Json.

## 2.2.1

### Date

* 2022.07.25

### Fixed
* Fixed so that dispose warning does not appear

## 2.2.0

### Date

* 2022.07.13

### Added
* Added Log On/Off
* Added LogLevel setting

## 2.1.2

### Date

* 2022.07.06

### Update

* Improved internal logic.

## 2.1.1

### Date

* 2022.06.07

### Update
* Improved to apply overwrite by default when importing

## 2.1.0

### Date

* 2022.05.30

### Added
* Added network and coroutine management function

## 2.0.9

### Date

* 2022.03.10

### Updated
* Explicitly improved FileStream Access permissions [(#184)](https://github.com/nhn/gpm.unity/issues/184)

## 2.0.8

### Date

* 2021.12.17

### Fixed
* Fixed warning issue when building
* Fixed typo in coroutine object variable

## 2.0.7

### Date

* 2021.12.13

### Added
* Added support for json Single type

### Changed
* Modified to make multiLanguage Loader extensibility
* Improved indicator logic

## 2.0.6

### Date

* 2021.09.01

### Fixed

* Fixed the script file name with the same name as Unity build-in component

## 2.0.5

### Date

* 2021.08.30

### Fixed

* Fix Unity package import failure issue
* Compatible with .net runtime 4.0 or lower

## 2.0.4

### Date

* 2021.07.05

### Fixed

* Fixed by compile error in Unity 2020.2

---

## 2.0.3

### Date

* 2021.07.05

### Fixed

* Fixed UnityWebRequest isNetworkError API being deprecated after Unity2020.2

---

## 2.0.2

### Date

* 2021.05.17

### Changed

* Changed internal indicators

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

* Brand name changed to Game Package Manager from TOAST Kit.

---

## 1.0.1

### Date

* 2020.08.21

### Added

* Add Compress module
* Multilanguage - Add GetSystemLanguage API

### Updated

* Minimum supported Unity version is now 2018.4.0
* Remove SharpZipLib.dll
* Multilanguage - Display the system language if it's supported.

---

## 1.0.0

### Features

* Multilanguage
* Indicator
* Log
* JSON parser