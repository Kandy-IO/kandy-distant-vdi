# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI

As part of the [Kandy VDI Tookit](https://github.com/Kandy-IO/kandy-vdi-toolkit), the Kandy Distant Driver for VDI enables application developers to deliver a HD experience for video and audio calls in a Citrix VDI environment. This driver adds support for the [Citrix Workspace App](https://docs.citrix.com/en-us/citrix-workspace-app.html) on [eLux OS](https://www.unicon-software.com/products/elux/) for use on thin clients.

### Configuration

The configuration is loaded from /setup/kandy.ini

#### RibbonRTC

This section allow to set different configuration flags that affect the browser container.

- CachePath: location where to store the application cache. defaults to: /tmp/kandy/cache
- CommandSwitch: Command Switch arguments to be used withthe browser container.
- DebugPort: Debug port to be used. If no port is provided the debug port is disabled. This value can be changed by the Debbugging tool FPM.
- LogPath: location where to store the application log (rtc.log). defaults to: /var/log/kandy
- VerboseLevel: level to which to enable the logs. Level can be from 0 to 10. Is the equivalent of the --v command line switch for the browser container. Overrides the LogLevel option.
- VerboseModules: Allows to filter the verbose logs that will be logged. Is the equivalent of the --vmodule command line switch for the browser container. setting it to */rtc/*=1 will enable logs for each of the rtc files that have a verbose level of 1. Overrides the LogLevel option.
- LogLevel: Level for which logs are stored. the value can be normal (default), verbose, warning and error.


#### Modules

This section allows to disable the Citrix Module in module.ini

RibbonRTC=Off will disable the RTC.DLL from being loaded by the Citrix Workspace App for Linux.

#### Certificates

This section allows to indicate which certificate files to load.

The name of a section and an indication wether it is On or Off needs to be use here. The section must contain the File and the Trustargs attributes.

#### Sample
[RibbonRTC]

CachePath=/tmp/kandy/cache

CommandSwitch=disable-extensions,disable-gpu

DebugPort=9222

LogPath=/var/log/kandy

VerboseLevel=1

VerboseModules=*/rtc/*=1,*/webrtc/*=1

LogLevel=normal

[Modules]

RibbonRTC=Off

[Certificates]

JPMCROOTCA=On

[JPMCROOTCA]

File=/setup/cacerts/JPMCROOTCA.pem

Trustargs=C,,
