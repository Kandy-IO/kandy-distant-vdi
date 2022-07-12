# Change Log

Kandy Distant Driver for VDI Mac change log.

- This change log follows [keepachangelog.com](http://keepachangelog.com/) recommendations.
- This project adheres to [Semantic Versioning](http://semver.org/).

## 1.7.0 - 2022-07-12

### Added
- Support for multiple distant sessions. `KAJ-1030`
- Logs to indicate if orchestrator fails to open. `KAJ-1164`

### Fixed
- Issue when comming out of sleep / hibernate. `KAJ-1247`
- Commlink Crash on launching Citrix session. `KAJ-1340`
- Distant Reinitialization fails during Virus Scan. `KAJ-1299`
- Orchestrator process does not close after browser crash. `KAJ-716`
- Browser Message Handler alters session state. `KAJ-1303`
- Quickly closing a session right after opening it will cause the VDI solution to freeze. `KAJ-1009`
- Opening and closing sessions multiple times can cause the Window to disapear. `KAJ-1007`

- Distant steals focus from CitrixViewer upon creation. `KAJ-930`
- Distant steals focus from CitrixViewer when clicked. `KAJ-937`
- Distant window has the wrong size when minimizing/unminimizing. `KAJ-1222`
- Distant windows blocks auxiliairy Citrix windows (About, Preferences, Exit, Taskbar). `KAJ-1084` `KAJ-1166` `KAJ-1167` `KAJ-1231` `KAJ-1310`
- Display issues in fullscreen mode. `KAJ-1163` `KAJ-1112`
- Display issues with multiple monitors. `KAJ-1165` `KAJ-1113` `KAJ-1050`


## 1.2.0 - 2022-03-18

### Fixed
- Browser stays opened when orchestrator crashes. `KAJ-971`
- Mac session cannot start if Citrix window is not in focus. `KAJ-936`
- Orchestrator does not allow browser to restart when browser crashes. `KAJ-716`
- Multiple session with the same id can be created. `KAJ-1034`
- Incorrect window matching. `KAJ-1011`
- Orchestrator & Browser get stuck waiting for each others' heartbeat. `KAJ-1029`
- Distant windows closes prematurely on Mac. `KAJ-1067`
- Browser error message not sent over IPC. `KAJ-1085`
- Orchestrator crashes after quickly creating and stopping distant sessions. `KAJ-1009`
- M1's very first send init command does not cause slowdowns and heartbeat failures anymore. `KAJ-1009`
- Dead unresponsive window remains visible when renderer process terminates. `KAJ-1098`
- Orchestrator does not handle browser death correctly causing recovery mechanism to not run. `KAJ-1128`
- Trailing directory separator in log path causes issues on some machines. `KAJ-1157`
- Send message to remote app when window closes. `KAJ-1039`
- Browser messages get buffered to prevent lost messages. `KAJ-1023`
- Unable to create new session after connection to remote is lost. `KAJ-1047`

### Added
- Multi-session support. `KAJ-1007`
- Remote App can close session in via `distant.close()`. `KAJ-1103`
- Session is closed when corresponding renderer process crashes. `KAJ-1105`

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
- `openOnly` flag can be used on the DistantBrowser executable which will run the initial one-time loading of the CEF library and exits immediatly. To be used by customer's install script. `KAJ-954` & `KAJ-990`

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
