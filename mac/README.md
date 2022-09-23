# @kandy-io/kandy-distant-vdi

# Kandy Distant Driver for VDI Mac (Plugin)
This driver adds support for [Citrix Workspace App for Mac](https://www.citrix.com/downloads/workspace-app/mac/workspace-app-for-mac-latest.html).

Please note that Citrix refers to Virtual Drivers as "Plugins" when referring to their use on MacOS.
## 1. Requirements
MacOS 10+ (Mojave and newer) 64 bit

Citrix Workspace App for Mac 2012 (tested on 2106 in release 1.0.0)

Dual Core CPU with 4 GB RAM recommended (equivalent to MacBook Air 2015 and newer)

## 2. Installation

### 2.1 Preparing Installation Files
If your Kandy Distant Driver is archived, expand the archive to yield the included files.

### 2.2 Signing
To assist in signing the product components, the following 3 plist files are provided:
- `entitlements-dylibs.plist`
- `entitlements-browser.plist`
- `entitlements-helpers.plist`

### 2.3 Sign the Plugin
The plugin and its dependent dynamic libraries must be signed.
*Please note that you will need to modify paths to suit your directory structure*

Run the following commands:
- `codesign -f --timestamp -o runtime --entitlements entitlements-dylibs.plist -s "YOUR CERTIFICATE NAME" <source path>/KandyDistant.PlugIn/Contents/Frameworks/libzmq.5.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" KandyDistant.PlugIn`

Signing can be verified with the following commands:
- `codesign --verify --deep --strict --verbose=2 <source path>/KandyDistant.PlugIn/Contents/Frameworks/libzmq.5.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/KandyDistant.PlugIn`

### 2.4 Sign the Applications
#### 2.4.1 Browser
Sign the dynamic libraries by running the following commands:
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libEGL.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libGLESv2.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libswiftshader_libEGL.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libswiftshader_libGLESv2.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libvk_swiftshader.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework`

Signing can be verified with the following commands:
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libEGL.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libGLESv2.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libswiftshader_libEGL.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libswiftshader_libGLESv2.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework/Libraries/libvk_swiftshader.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/Chromium\ Embedded\ Framework.framework`

Sign the Browser Helper applications by running the following commands:
- `codesign -f --timestamp -o runtime --entitlements src/browser/mac/entitlements-helpers.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper.app`
- `codesign -f --timestamp -o runtime --entitlements src/browser/mac/entitlements-helpers.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper\ \(GPU\).app`
- `codesign -f --timestamp -o runtime --entitlements src/browser/mac/entitlements-helpers.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper\ \(Plugin\).app`
- `codesign -f --timestamp -o runtime --entitlements src/browser/mac/entitlements-helpers.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper\ \(Renderer\).app`
- `codesign -f --timestamp -o runtime --entitlements src/browser/mac/entitlements-browser.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantBrowser.app`

Signing can be verified with the following commands:
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper.app`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper\ \(GPU\).app`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper\ \(Plugin\).app`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app/Contents/Frameworks/DistantBrowser\ Helper\ \(Renderer\).app`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantBrowser.app`

#### 2.4.2 Orchestrator
Sign the dynamic library with the following command:
`codesign -f --timestamp -o runtime --entitlements entitlements-dylibs.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantOrchestrator.app/Contents/Frameworks/libzmq.5.dylib`

Sign the Orchestrator application with the following command:
`codesign -f --timestamp -o runtime --entitlements entitlements-dylibs.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantOrchestrator.app`

Verify signing with the following commands:
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantOrchestrator.app/Contents/Frameworks/libzmq.5.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantOrchestrator.app`

### 2.5 (OPTIONAL) Create Apple Disk Image
Should you choose to build your own Apple Disk Image (DMG) for your own purposes, you can follow these steps:
1. Create an input folder
2. Create an output folder
2. Copy the plugin and applications to the input folder:
  - `KandyDistant.PlugIn`
  - `DistantOrchestrator.app`
  - `DistantBrowser.app`
3. Create the disk image with the following command:
`hdiutil create -srcFolder <input folder> -quiet -volname KandyDistant -o <output folder>/KandyDistant.dmg`
4. Sign the disk image:
`codesign -f --timestamp -s "YOUR CERTIFICATE NAME" <output folder>/KandyDistant.dmg`
5. Verify signing:
`codesign --verify --deep --strict --verbose=2 <output folder>/KandyDistant.dmg`

## 3. Installing

### 3.1 Citrix Workspace App
It is expected that you have installed [Citrix Workspace App for Mac](https://www.citrix.com/downloads/workspace-app/mac/workspace-app-for-mac-latest.html).


### 3.2 Installing Files
1. Ensure that you have created destination directories for the **plugin** and **applications**
2. Copy the plugin to your preferred Citrix plugins directory:
`cp -R <source path>/KandyDistant.PlugIn <plugin destination path>`
3. Copy the 2 applications to the Kandy Application Support directory:
- `cp -R <source path>/DistantOrchestrator.app <application destination path>`
- `cp -R <source path>/DistantBrowser.app <application destination path>`

## 4. Configuration

### 4.1 Setup
*The Citrix Workspace App must be configured to load the KandyDistant plugin*
The configuration file for the Citrix Workspace App can be found here:
`~/Library/Application\ Support/Citrix\ Receiver/Modules`

Edit the `Modules` to add the necessary settings:
1. Open `~/Library/Application\ Support/Citrix\ Receiver/Modules`
2. Locate the `[ICA 3.0]` section
3. Append the KandyDistant plugin to the `VirtualDriver` key. It should look similar to the following:
`VirtualDriver=Thinwire3.0, TWI, SmartCard, SSPI, TUI, KandyDistant.PlugIn`
4. Under the same section (`[ICA 3.0]`), add a key for our plugin and assign it the value of "On":
`KandyDistant.PlugIn=On`
5. Add a section for our plugin (and optionally set your custom executable path):
```
[KandyDistant]
ExecutablePath = /your/path/
```

### 4.2 Modifying Citrix Configuration
LogPath and LogLevel can be added and modified under the KandyDistant section.

ex:
- LogPath  = ~/Kandy/logs
- LogLevel = debug

LogPath will default to `~/Library/Application Support/Kandy/logs`
LogLevel will default to `info`

Accepted log level values are:
- off
- critical
- error
- warn
- info
- debug
- trace

### 4.3 KandyLib Configuration
KandyLib-specific configuration can be set and modified in your `config ini` file which is expected to be found in the path provided as `ExecutablePath` in your Citrix configuration file (`Modules`):

The `KandyDistant` section allows configuration flags that affect the browser container to be set.

- CachePath: location where to store the application cache, defaults to: ~/Library/Application Support/Kandy/cache.
- CommandSwitch: Optional Command Switch arguments to be used with the browser container. Multiple command switches can be separated by a comma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.
- ExecutablePath: The absolute path to your execution path and configuration file
- SessionOverwrite: When enabled, the Kandy Distant Driver handles Session Start requests by creating a new session which overwrites any existing session. Accepted values are: `true`, `false` (default)
- CefLogLevel: Log level used by CEF. Defaults to `info`. Other available choices are `trace`, `debug`, `info`, `warn`, `error`, `critical`, or `off`. `debug` option will display verbose level 1 CEF logs.
- VerboseLevel: Number flag indicating how verbose the CEF logs will be. Only supports `1`.
- VerboseModules: Number flag indicating how verbose CEF logs will be on a per module basis. Where the modules are chromium modules and can be found here https://source.chromium.org/chromium/chromium/src. Number used can range from `1` to `3` and `-3` for filtering out modules. For this to work, VerboseLevel must be set to `1`.


### 4.4 Sample (config.ini)
```
[KandyDistant]
CachePath=~/Library/Application Support/Kandy/cache
CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu
DebugPort=9222
ExecutablePath=/your/path
SessionOverwrite=false
CefLogLevel=debug
VerboseLevel=1
VerboseModules=*webrtc*=1,*=-3
```
In this example, VerboseModules will show verbose level 1 webrtc logs and will filter out all other modules.


## 5. Before Running
Make sure that you have created appropriate directories for the KandyDistant log and the browser cache. These values should match your configuration of the Citrix `Modules` file.
Default values are:
- `~/Library/Application Support/Kandy/logs`
- `~/Library/Application Support/Kandy/cache`

On M1, you can run the DistantBrowser executable with the `openOnly` flag.
This is so that the initial one-time loading of the CEF library, which may take a several seconds, can happen.

Congratulations! You have built, signed, installed and configured the KandyDistant plugin for Citrix Workspace App on MacOS!

### 6. Logs
By default, the logs can be found at `~/Library/Application Support/Kandy/logs`.

#### 6.1 Log Rotation
Each time the VDI driver is run, log files with the following format will be created:
- `distant-<pid>.log` - The vdi driver logs.
- `browser_console-<pid>.log` - The browser process CEF logs.

When the VDI Driver is run, log files that are 7 or more days old will be deleted.

## 7. User Environment
### 7.1 Multiple Display Configuration
The Kandy Distant Driver for VDI supports multiple displays as of version 1.7

#### **<u>Important</u>**
*For proper FULLSCREEN operation, you should configure Mission Control to use **separate spaces**. <u>This is the default setting in MacOS</u>*

Here are the steps to optimize Misson Control for FULLSCREEN mode:
1. Open System Preferences -> Mission Control
2. Ensure the checkbox next to "`Displays have separate Spaces`" is **CHECKED**/**ACTIVE**

## 8. Sleep & Disconnect
CWA (Citrix Workspace App) handles computer sleep and network disconnects somewhat differently on each OS. This has some impact on Distant and your Distant sessions. It is important that your application can handle these scenarios. Please refer to the subsections for more information.

### 8.1 Sleep
When waking from a short sleep (less than approximately 3 minutes) the CWA will resume and your original Distant session will be available.

When waking from a long sleep (more than approximately 3 minutes) :
 - The CWA may exit in which case your Distant session will be closed.
 - The CWA may exit and restart in which case your Distant session may be reloaded, or closed.

### 8.2 Disconnect
When reconnected after being disconnected for a duration of under 3 minutes, the CWA will resume and your original Distant session will be available.

When reconnected after being disconnected for a duration of more than 3 minutes, the CWA will resume and your Distant session may be reloaded.

When still disconnected for more than 5 minutes, the CWA your Distant session will be closed. The user will need to open a new Citrix connection and create a new session once they have an internet connection.

## 9. Known Issues / Limitations
### Known Issues
- No local and remote video seen on video call when the vdi mac recovers from "sleep"  action after 4 minutes. `KAJ-1127`
- The remote app window functions best in fullscreen mode when Mission Control's *Displays have separate Spaces* is set to the default *checked* setting
- The remote app window functions best in fullscreen mode when Citrix is configured to use ALL monitors. `KAJ-1314`