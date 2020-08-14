# Change Log

Kandy WebRTC VDI Toolkit, Citrix Driver change log.

- This change log follows [keepachangelog.com](http://keepachangelog.com/) recommendations.
- This project adheres to [Semantic Versioning](http://semver.org/), however, eLux packages also include a -X identifier, which represents the version of the eLux package

## 1.5.1-0 - 2020-08-14
### Fixed
- Keyboard focus is getting stolen from the VDI session when clicking on the overlay video.

### Changed
- Updated the code siging certificate to Ribbon Communications Canada ULC

Note that a 32-bit (RP5) version was not released

## 1.5.0-0 - 2020-03-05
### Added
- A 64-bit (RP6) version of this package is available

Note that a 32-bit (RP5) version was not released

## 1.4.0-3 - 2020-01-17
### Fixed
- Regression with the log location.

## 1.4.0-2 - 2020-01-10

### Fixed

- Interroperability issue with other packages on eLux RP5

## 1.4.0-0 - 2019-11-06

### Changed

- Change the configuration to be loaded from /setup/kandy.ini
- Change the log level of most logs to use verbose level. KAJ-133

### Added

- Added Log rotation so that /var/log/kandy/rtc.log is copied to rtc-n.log on startup KAJ-71

## 1.3.0-0 - 2019-10-04

### Added

- Added the ability to import certificates to the certificate store
- Added fpm to disable the logs

## 1.2.2-0 - 2019-08-01

### Fixed

- Remove logs from Elux Install Script KAA-1902
- Interoperability with Kandy HID Driver KAA-1875

### Added

- Added Description for the Elux package KAA-1931
- Ability to Debug the Remote application via an Optional package KAA-1893

## 1.2.1-0 - 2019-06-27

### Fixed

- Session Crash on broken pipe `KAA-1784`
- Crash on Closing session with FillPacketVirtualWrites `KAA-1809`
- Crash on closing the driver, due to packetization destructor `KAA-1883`
- Regression, window is shown on move window `KAA-1812`

## 1.2.0-0 - 2019-06-10

### Added

- Added configurable cache folder, and configurable Chromium command line switches `KAA-1631`
- Added configurable debugger port (disabled by default) `KAA-1623`
- Added missing V8 context snapshot cache file for faster loading. `KAA-1746`

### Changed

- Updated the Virtual Channel SDK version to 13.10 from 13.8 `KAA-1631`
- Use of the correct version of the Virtual Channel SDK library, depending on the build type `KAA-1624`
