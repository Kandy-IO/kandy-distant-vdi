# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI Mac

This driver adds support for [Citrix Workspace App for Mac](https://www.citrix.com/downloads/workspace-app/mac/workspace-app-for-mac-latest.html).

### Requirements

MacOS 10+ (Mojave and newer) 64 bit

Citrix Workspace App for Mac 2012 (tested on 2106 in release x.x.x)

Dual Core CPU with 4 GB RAM recommended (equivalent to MacBook Air 2015 and newer)

### Limitations

Only 1 VDI session is permitted. In the event that a 2nd VDI session is requested, a Session Error response will be returned to the client application.

### Installation

#### Apple Disk Image

#### Install Script

The install.ps1 script is given as an example on how to install the files, and will setup the application with some defaults path. The script needs to be run as an administrator and will install the program into C:\Program Files\Kandy.

#### Files

### Configuration

Configuration is provided from two sources:

#### Citrix Configuration
The Citrix Workspace App provides a Citrix Receiver component with a configuration file available in the Application Support files on your system. This is typically found here:
- ~/Library/Application Support/Citrix Receiver/Modules

LogPath and LogLevel can be added and modified under the KandyDistant section.

ex:
- LogPath  = ~/Kandy/logs
- LogLevel = debug

LogPath will default to ~/Library/Application Support/Kandy/logs
LogLevel default to info and can be set to:
- off
- critical
- error
- warn
- info
- debug
- trace

#### KandyLib Configuration
KandyLib-specific configuration can be set and modified in a config ini file which is expected to be found here:
- ~/Library/Application Support/Kandy/config.ini

The `RibbonRTC` section allows configuration flags that affect the browser container to be set.

- CachePath: location where to store the application cache, defaults to: ~/Library/Application Support/Kandy/cache.
- CommandSwitch: Optional Command Switch arguments to be used with the browser container. Multiple command switches can be separated by a comma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.

#### Sample (config.ini)

[RibbonRTC]

CachePath=c:\tmp\cache

CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu

DebugPort=9222
