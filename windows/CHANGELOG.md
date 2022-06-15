# Change Log

Kandy Distant Driver for VDI Windows change log.

- This change log follows [keepachangelog.com](http://keepachangelog.com/) recommendations.
- This project adheres to [Semantic Versioning](http://semver.org/).


## 1.7.0 - 2022-06-07

### Added
- Multiple session with the same id can be created. `KAJ-1034`
- Reinit Commlink/Orch when heartbeat is missed. `KAJ-1247`
- Improved multi-session support on browser process. `KAJ-1118`
- Logs will indicate if orchestrator fails to open. `KAJ-1164`

- Windows: Handle browser process not opening and log the error. `KAJ-541`
- Windows: Executables produce a dump file on system exceptions. `KAJ-1155`

### Fixed
- Orchestrator process does not close after simulating browser crash. `KAJ-716`
- Distant Reinitialization fails during Virus Scan. `KAJ-1299`
- Browser Start Success doesn't persist all session properties. `KAJ-1307`
- Browser Message Handler alters session state. `KAJ-1303`

- Windows: Browser crashes on Close Session. `KAJ-1280`
- Windows: Browser exits unexpectedly during initialization. `KAJ-1274`
- Windows: Unable to click on Citrix & CEF window during call. `KAJ-1230`
- Windows: `VerboseLevel` & `VerboseModules` flag now take effect & get passed to CEF. `KAJ-1177`
- Windows: Click event not being processed. `KAJ-1048`


## 1.1.3 - 2022-01-11

### Fixed

- Cannot reconnect after sleep. `KAJ-916`
- Two orchestrator instances after system sleep. `KAJ-947`
- Video Calls stuck in Initiating. `KAJ-955`
- Build information is missing from logs. `KAJ-1082`

### Added

- Report http connection end error (i.e DNS error). `KAJ-948`

## 1.1.2 - 2021-11-18

### Fixed

- Multiple Distant Start attempts can happens concurrently. `KAJ-879`
- Browser does not exit by itself. `KAJ-906`
- Cannot reconnect after hibernate. `KAJ-919`
- Orchestrator does not exit if browser crashes during shutdown. `KAJ-924`
- Browser retries unreachable URL in loop. `KAJ-926`
- Citrix viewer crash on close. `KAJ-934`
- Status is incorrectly reported as closed. `KAJ-1081`

## 1.1.1 - (Not Released)

### Fixed

- Multiple Static initialization issues. `KAJ-638`
- Orchestrator window opening on Windows. `KAJ-638`
- Log timestamps are not in order. `KAJ-900`
- Browser cannot start on other drive letters.`KAJ-892`
- Browser Console logs are not in the right location. `KAJ-897`

### Changed

- Updated the configuration to use KandyDistant instead of RibbonRTC. `KAJ-809`

## 1.1.0 - 2021-09-02

### Fixed

- CEF Verbose log not working. `KAJ-675`
- Hibernation or Sleep while the VDI session is open could lead to the VDI Driver not working on wake. `KAJ-676`
- Video is over the Citrix Disconnect button. `KAJ-753`
- High Latency causes Browser Renderer to Crash. `KAJ-757`
- Commlink logs are missing. `KAJ-791`
- Session status reported as ready before the page is loaded. `KAJ-792`
- Log and cache path cannot contain spaces. `KAJ-857`

### Added

- Add event for when session fails to load. `KAJ-56`
- Log rotation. `KAJ-673`
- Logs now report issues about opening processes and ports conflicts. `KAJ-774`
- CefLogLevel as a configuration. `KAJ-810`

### Changed

- Allow session overwrite (allows session to be created even if a session already exist by deleting all existing session). `KAJ-772`
- Updated the Chrome Embedded Framework to version 91. `KAJ-796`
- Updated Citrix VCSDK to 2107. `KAJ-798`
- Performance improvements for message queue. `KAJ-808`

## 1.0.0 - 2021-03-10

### Added

- Support for Windows 10 64 bit.
