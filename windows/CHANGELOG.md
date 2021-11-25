# Change Log

Kandy Distant Driver for VDI Windows change log.

- This change log follows [keepachangelog.com](http://keepachangelog.com/) recommendations.
- This project adheres to [Semantic Versioning](http://semver.org/).

## 1.1.2 - 2021-11-18

## 1.1.1 (Not Released)

## 1.1.0 - 2021-09-02

### Fixed

- Log and cache path cannot contain spaces. `KAJ-857`
- Session status reported as ready before the page is loaded. `KAJ-792`
- High Latency causes Browser Renderer to Crash. `KAJ-757`
- CEF Verbose log not working. `KAJ-675`
- Commlink logs are missing. `KAJ-791`
- Video is over the Citrix Disconnect button. `KAJ-753`
- Hibernation or Sleep while the VDI session is open could lead to the VDI Driver not working on wake. `KAJ-676`

### Added

- Add event for when session fails to load. `KAJ-56`
- Logs now report issues about opening processes and ports conflicts. `KAJ-774`
- CefLogLevel as a configuration. `KAJ-810`
- Log rotation. `KAJ-673`

### Changed

- Updated the Chrome Embedded Framework to version 91. `KAJ-796`
- Updated Citrix VCSDK to 2107. `KAJ-798`
- Performance improvements for message queue. `KAJ-808`
- Allow session overwrite (allows session to be created even if a session already exist by deleting all existing session). `KAJ-772`

### Known Issues

- Interaction with the Kandy Distant VDI remote window with mouse or keyboard is not working. `KAJ-613`

## 1.0.0 - 2021-03-10

### Added

- Support for Windows 10 64 bit.

### Known Issues

- Interaction with the Kandy Distant VDI remote window with mouse or keyboard is not working. `KAJ-613`
- Hibernation or Sleep while the VDI session is open could lead to the VDI Driver not working on wake. `KAJ-676`
