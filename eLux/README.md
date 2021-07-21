# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI eLux

This driver adds support for [Citrix Workspace App for Linux](https://docs.citrix.com/en-us/citrix-workspace-app-for-linux.html) on [eLux OS](https://www.unicon-software.com/products/elux/) for use on thin clients.

Note that eLux RP5 is not actively maintained.

### eLux Package Signature

You can download the following Root and Code Signing CA certificate from digicert

DigiCert Assured ID Root CA:

https://cacerts.digicert.com/DigiCertAssuredIDRootCA.crt.pem

DigiCert SHA2 Assured ID Code Signing CA:

https://cacerts.digicert.com/DigiCertSHA2AssuredIDCodeSigningCA.crt.pem

### Browser Container Certificates

eLux 6.9 provides certificate management directly in the OS for our browser container. If there is a need to use custom certificates for reaching https websites in the browser container please ignore the Certificate Configuration below and put the certificate in the /setup/cacerts/browser folder as mentioned in the eLux [Documentation](https://www.unicon-software.com/udocs/en/#admin_guides/scout_enterprise/app_definition/browser/browser_config.htm?Highlight=cacert).

### Configuration

The configuration is loaded from /setup/kandy.ini

#### RibbonRTC

This section allow to set different configuration flags that affect the browser container.

- CachePath: location where to store the application cache. defaults to: /tmp/kandy/cache
- CommandSwitch: Command Switch arguments to be used with the browser container.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled. This feature can also be enabled by the optional eLux package "Enable development tools" which will use the value 9222.
- LogPath: location where to store the application log (rtc.log). defaults to: /var/log/kandy
- VerboseLevel: level to which to enable the logs. Level can be from 0 to 10. Is the equivalent of the --v command line switch for the browser container. Overrides the LogLevel option.
- VerboseModules: Allows to filter the verbose logs. Is the equivalent of the --vmodule command line switch for the browser container. setting it to */rtc/*=1 will enable logs for each of the rtc files that have a verbose level of 1. Overrides the LogLevel option.
- LogLevel: Level for which logs are stored. the value can be normal (default), verbose, warning and error.
- SessionOverwrite: When enabled, the Kandy Distant Driver handles Session Start requests by creating a new session which overwrites any existing session. Accepted values are: `true`, `false` (default)


#### Modules

This section allows to disable the Citrix Module in module.ini

RibbonRTC=Off will disable the RTC.DLL from being loaded by the Citrix Workspace App for Linux.

#### Certificates (eLux < 6.9 only)

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

CACERT1=On

INTERMEDIATECERT1=On

[CACERT1]

File=/setup/cacerts/CACERT1.pem

Trustargs=C,,

[INTERMEDIATECERT1]

File=/setup/cacerts/INTERMEDIATECERT1.pem

Trustargs=,,,
