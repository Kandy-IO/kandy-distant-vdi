# Change Log

Kandy Distant Driver for VDI Mac change log.

- This change log follows [keepachangelog.com](http://keepachangelog.com/) recommendations.
- This project adheres to [Semantic Versioning](http://semver.org/).

## [Unreleased]

- Orchestrator process does not close after simulating browser crash. `KAJ-716`
- Mac session cannot start if Citrix window is not in focus. `KAJ-936`
- Browser stays opened when orchestrator crashes. `KAJ-971`
- Distant messges sent too quickly causes issues on M1. `KAJ-1023`
- Multiple session with the same id can be created. `KAJ-1034`
- Distant windows closes prematurely on Mac. `KAJ-1067`

## 1.1.4 - 2021-12-07

### Fixed

- Build information is missing from logs. `KAJ-1082`

## 1.1.3 - 2021-12-06

### Fixed

- Cannot reconnect after sleep. `KAJ-916`
- Cannot reconnect after hibernate. `KAJ-919`
- Citrix viewer crash on close. `KAJ-934`
- Two orchestrator instances after system sleep. `KAJ-947`
- Citrix Viewer crashes after sleep > 3 minutes. `KAJ-951`
- M1 Fresh Install Browser Process Initial Delay. `KAJ-954`
- Video Calls stuck in Initiating. `KAJ-955`

### Added

- Report http connection end error (i.e DNS error). `KAJ-948`

## 1.1.2 - 2021-11-08

### Fixed

- Browser proecess crash on close. `KAJ-920`
- Orchestrator may crash on shutdown. `KAJ-931`
- Orchestrator hangs on Shutdown. `KAJ-932`
- Session should fail when window is not available on Mac. `KAJ-933`

## 1.1.1 - 2021-11-05

### Fixed

- Orchestrator does not exit if browser crashes during shutdown. `KAJ-924`
- Browser crash during shutdown.`KAJ-925`
- Browser retries unreachable URL in loop. `KAJ-926`
- Status is incorrectly reported as closed. `KAJ-1081`

## 1.1.0 - 2021-11-01

### Fixed

- Static initialization issues. `KAJ-638`
- Citrix crash when the app resumes from sleep. `KAJ-714`
- Flickering issue. `KAJ-750`
- Video comes out of the Citrix Window. `KAJ-752`
- Disconnect button stays behind the video.`KAJ-753`
- High Latency causes Browser Renderer to Crash. `KAJ-757`
- Logs now report issues about opening processes and ports conflicts. `KAJ-774`
- Multiple protocol issues. `KAJ-787`
- Comlink logs are missing. `KAJ-791`
- Session event READY should be sent when page finish loading. `KAJ-792`
- Multiple Distant Start attempts can happens concurrently. `KAJ-879`
- Log timestamps are not in order. `KAJ-900`
- Browser process does not close properly. `KAJ-905`

### Added

- Enable CEF Verbose log. `KAJ-675`
- Session Overwrite feature. `KAJ-772`
- Dynamic port allocation. `KAJ-780`
- Add CEFLogLevel as a configuration. `KAJ-810`
- Allow Browser to start for Mac Verification with openOnly flag. `KAJ-907`
- Versioning for Mac bundles. `KAJ-918`

### Changed

- Reduce the number of ports use by the application. `KAJ-779`
- Updated the configuration to use KandyDistant instead of RibbonRTC. `KAJ-809`

## 1.0.0 - 2021-07-08

### Added

- Support for MacOS 10+ (Mojave and newer) 64 bit
