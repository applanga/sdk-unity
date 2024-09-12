# Applanga SDK for Unity CHANGELOG
***
*Website:* <https://www.applanga.com> 

*Applanga Unity Documentation:* <https://www.applanga.com/docs-integration/unity> 
***

### Version 2.0.94 (12 Sep 2024)
#### Added
- Added branching to the Unity SDK
- Added a screenshot menu toggle button to the inspector view in the Unity editor
- Added a draft mode activation dialog toggle button to the inspector view in the Unity editor
- Added draft mode activation dialog toggle keyboard shortcuts

#### Fixed
- Fixed the screenshot menu toggle keyboard shortcuts
- Fixed bug where it was not possible to switch to a branch if a settings file had never been opened with that branch as the default branch.

---
### Version 2.0.91 (25 Jan 2024)
#### Fixed
- Added integration header

---
### Version 2.0.90 (1 Sep 2023)
#### Fixed
- Resolved did issue on huawei phones

---
### Version 2.0.89 (30 Jun 2023)
#### Fixed
- Resolved caching issues with draft values

---
### Version 2.0.87 (23 Jun 2023)
#### Fixed
- Fixed values not properly return for draft mode

---
### Version 2.0.79 (19 Nov 2022)
#### Fixed
- Fixed deprecated methods and dependencies

---
### Version 2.0.76 (7 Jun 2022)
#### Fixed
- Fixes issue when user destroys Applanga object manually, by catching and giving a warning to user 
- Fixes null reference exception on XRSettings on iOS builds 

---
### Version 2.0.74 (6 May 2022)
#### Fixed
- Changed Applanga UnitySDK dependencies to .net 4.6.1, solves issue with hard reference to .net 2.0.0
- Changes fetching of Mono.Data.SQL.dll according to platform and Unity version
- Changed a deprecated method to current version for fetching iOS device target 

---
### Version 2.0.73 (20 Apr 2022)
#### Fixed
- Changed missing settings file errors to warnings for more user friendly indicator
- Changes fetching of Mono.Data.SQL.dll to unity-jit according to platform
- Fixes all current issues with creation and deletion of DB's on Sqlite

---
### Version 2.0.72 (8 Apr 2022)
#### Fixed
- Removed use of gzip compression for Windows platform
- Hotfix for issue with db delete

---
### Version 2.0.71 (15 Jul 2021)
#### Fixed
- Font not properly shown for embedded Sample Scene

---
### Version 2.0.70 (9 Jul 2021)
#### Added
- Error when key is too big
- Draft menu redesign

#### Fixed
- Unity 2020 compatibility and embedded demo project

---
### Version 2.0.69 (28 Jul 2020)
#### Fixed
- Automatic removal of language databases that dont exist on the dashboard
- Gzip enabled for get requests

---
### Version 2.0.67 (2 Apr 2020)
#### Fixed
- Changed all usages of the WWW class to use UnityWebRequests.


---
### Version 2.0.66 (2 Mar 2020)
#### Added
- Added DoNotTranslate string array to the DoNotTranslate and AutoTranslate components.
- Added support for TextMeshProUGUI Component

#### Fixed
- fix for preprocess build script in 2017


---
### Version 1.0.57 (30 Jan 2020)
#### Added

- automatic and manual setting file update menu items
- Including strings with missing keys when taking a screen shot
- Sending current language when reporting an issue

---
### Version 1.0.56 (2 Oct 2019)

#### Added

- added check for keys longer than 997 bytes to meet database requirements
- added check for new lines in keys
- added ApplangaDraftModeEnabled setting

#### Fixed
- Fixed Warnings for cleaning up auto created ApplangaObjects
- Fixed gesture tracking error when using mouse input in the editor

---
### Version 1.0.54 (11 Sep 2019)

- added ApplangaInitialUpdate setting
- BugFix: Unity android Gzip handling

---
### Version 1.0.53 (7 Jun 2019)
#### Added
- updates to work with latest unity version
- editor ui to add and remove AutoTranslate components
- intorduced DoNoTranslate component to ignore AutoTranslate component
- editor ui to configure id generation
- TextMeshPro support
- android il2cpp arm 64 bit support

---
### Version 1.0.44 (12 Jun 2018)
#### Added
- delta update support for smaller response size

---
### Version 1.0.43 (12 Jun 2018)
#### Fixed
- initialization error on iOS from Unity 2017.4 and Unity 2018

---
### Version 1.0.41 (21 Mar 2018)
#### Changed
- added docs link on component

---
### Version 1.0.40 (21 Mar 2018)
#### Changed
- update demoscene with language switch and testaccount

#### Fixed
- unity 2017.3 compatibility

---
### Version 1.0.39 (18 Dec 2017)
#### Fixed
- fixed possible request timeout when changing scenes

---
### Version 1.0.37 (14 Dec 2017)
#### Changed
- fixed accidental draftmode activation

---
### Version 1.0.36 (24 Nov 2017)
#### Changed
- added changelog
- added GetLanguage method to get current used language

---
#### Fixed
- local cache issue
- updated current language crash

---
### Version 1.0.35 (1 Nov 2017)
#### Fixed
- internal draft mode gesture exception

---
### Version 1.0.33 (13 Sep 2017)
#### Changed
- use Application.identifier or Application.bundleIdentifier depending on unity version

---
### Version 1.0.32 (6 Sep 2017)
#### Fixed
- string update issue
- i2 performance issue

---
### Version 1.0.30 (5 Sep 2017)
#### Fixed
- android build issues

---
### Version 1.0.29 (4 Sep 2017)
#### Changed
- i2 performance improvements

---
### Version 1.0.28 (2 Sep 2017)
#### Changed
- logger output support for old and new unity versions

---
### Version 1.0.26 (28 Aug 2017)
#### Fixed
- editor initialization issues

---
### Version 1.0.25 (25 Aug 2017)
#### Fixed
- linker issue
- i2 localization performance

---
### Version 1.0.21 (22 Aug 2017)
#### Changed
- added support for unity 2017.1

---
### Version 1.0.20 (21 Aug 2017)
#### Fixed
- unity version issue where bundleId method does not exist

---
### Version 1.0.19 (16 Aug 2017)
#### Changed
- updated unity sdk to be able to run in edit mode
- add bridge between Applanga an i2 localization

---
### Version 1.0.12 (11 Jul 2017)
#### Added
- basic mobile VR support for Google Cardboard

#### Fixed
- linker issue if stripping is enabled on Android

---
### Version 1.0.11 (13 Jun 2017)
#### Fixed
- iOS linker issues
- tests

---
### Version 1.0.7 (10 Mar 2017)
#### Fixed
- documentation

---
### Version 1.0.6 (8 Feb 2017)
#### Changed
- minor internal refactorings and stability improvements

---
### Version 1.0.3 (7 Feb 2017)
#### Fixed
- documentation
- deploy script
- sqlite issues

---
### Version 1.0.0  (30 Jan 2017)
#### Changed
- Initial Release

--- 
