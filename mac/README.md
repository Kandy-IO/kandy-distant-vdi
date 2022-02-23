# @kandy-io/kandy-distant-vdi

# Kandy Distant Driver for VDI Mac (Plugin)
This driver adds support for [Citrix Workspace App for Mac](https://www.citrix.com/downloads/workspace-app/mac/workspace-app-for-mac-latest.html).

Please note that Citrix refers to Virtual Drivers as "Plugins" when referring to their use on MacOS.
## 1. Requirements
MacOS 10+ (Mojave and newer) 64 bit

Citrix Workspace App for Mac 2012 (tested on 2106 in release 1.0.0)

Dual Core CPU with 4 GB RAM recommended (equivalent to MacBook Air 2015 and newer)

## 2. Limitations
Only 1 VDI session is permitted. In the event that a 2nd VDI session is requested, a Session Error response will be returned to the client application.

## 3. Installation

### 3.1 Preparing Installation Files
If your Kandy Distant Driver is archived, expand the archive to yield the included files.

### 3.2 Signing
To assist in signing the product components, the following 3 plist files are provided:
- `entitlements-dylibs.plist`
- `entitlements-browser.plist`
- `entitlements-helpers.plist`

### 3.3 Sign the Plugin
The plugin and its dependent dynamic libraries must be signed.
*Please note that you will need to modify paths to suit your directory structure*

Run the following commands:
- `codesign -f --timestamp -o runtime --entitlements entitlements-dylibs.plist -s "YOUR CERTIFICATE NAME" <source path>/KandyDistant.PlugIn/Contents/Frameworks/libzmq.5.dylib`
- `codesign -f --timestamp -o runtime -s "YOUR CERTIFICATE NAME" KandyDistant.PlugIn`

Signing can be verified with the following commands:
- `codesign --verify --deep --strict --verbose=2 <source path>/KandyDistant.PlugIn/Contents/Frameworks/libzmq.5.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/KandyDistant.PlugIn`

### 3.4 Sign the Applications
#### 3.4.1 Browser
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

#### 3.4.2 Orchestrator
Sign the dynamic library with the following command:
`codesign -f --timestamp -o runtime --entitlements entitlements-dylibs.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantOrchestrator.app/Contents/Frameworks/libzmq.5.dylib`

Sign the Orchestrator application with the following command:
`codesign -f --timestamp -o runtime --entitlements entitlements-dylibs.plist -s "YOUR CERTIFICATE NAME" <source path>/DistantOrchestrator.app`

Verify signing with the following commands:
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantOrchestrator.app/Contents/Frameworks/libzmq.5.dylib`
- `codesign --verify --deep --strict --verbose=2 <source path>/DistantOrchestrator.app`

### 3.5 (OPTIONAL) Create Apple Disk Image
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

## 4. Installing

### 4.1 Citrix Workspace App
It is expected that you have installed [Citrix Workspace App for Mac](https://www.citrix.com/downloads/workspace-app/mac/workspace-app-for-mac-latest.html).


### 4.2 Installing Files
1. Ensure that you have created destination directories for the **plugin** and **applications**
2. Copy the plugin to your preferred Citrix plugins directory:
`cp -R <source path>/KandyDistant.PlugIn <plugin destination path>`
3. Copy the 2 applications to the Kandy Application Support directory:
- `cp -R <source path>/DistantOrchestrator.app <application destination path>`
- `cp -R <source path>/DistantBrowser.app <application destination path>`

## 5. Configuration

### 5.1 Setup
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

### 5.2 Modifying Citrix Configuration
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

### 5.3 KandyLib Configuration
KandyLib-specific configuration can be set and modified in your `config ini` file which is expected to be found in the path provided as `ExecutablePath` in your Citrix configuration file (`Modules`):

The `KandyDistant` section allows configuration flags that affect the browser container to be set.

- CachePath: location where to store the application cache, defaults to: ~/Library/Application Support/Kandy/cache.
- CommandSwitch: Optional Command Switch arguments to be used with the browser container. Multiple command switches can be separated by a comma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.
- ExecutablePath: The absolute path to your execution path and configuration file
- SessionOverwrite: When enabled, the Kandy Distant Driver handles Session Start requests by creating a new session which overwrites any existing session. Accepted values are: `true`, `false` (default)

### 5.4 Sample (config.ini)
```
[KandyDistant]
CachePath=~/Library/Application Support/Kandy/cache
CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu
DebugPort=9222
ExecutablePath=/your/path
SessionOverwrite=false
```

## 6. Before Running
Make sure that you have created appropriate directories for the KandyDistant log and the browser cache. These values should match your configuration of the Citrix `Modules` file.
Default values are:
- `~/Library/Application Support/Kandy/logs`
- `~/Library/Application Support/Kandy/cache`

Congratulations! You have built, signed, installed and configured the KandyDistant plugin for Citrix Workspace App on MacOS!
