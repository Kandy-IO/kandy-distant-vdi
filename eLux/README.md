# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI eLux

This driver adds support for [Citrix Workspace App for Linux](https://docs.citrix.com/en-us/citrix-workspace-app-for-linux.html) on [eLux OS](https://www.unicon-software.com/products/elux/) for use on thin clients.

### 1. eLux Package Signature

You can donwload the following Root and Code Signing CA certificate from digicert

DigiCert Assured ID Root CA:

https://cacerts.digicert.com/DigiCertAssuredIDRootCA.crt.pem

DigiCert SHA2 Assured ID Code Signing CA:

https://cacerts.digicert.com/DigiCertSHA2AssuredIDCodeSigningCA.crt.pem

### 2. Browser Container Certificates

eLux 6.9 provides certificate management directly in the OS for our browser container. If there is a need to use custom certificates for reaching https websites in the browser container please ignore the Certificate Configuration below and put the certificate in the /setup/cacerts/browser folder as mentioned in the eLux [Documentation](https://www.unicon-software.com/udocs/en/#admin_guides/scout_enterprise/app_definition/browser/browser_config.htm?Highlight=cacert).

### 3. Configuration

#### 3.1 Setup
*The Citrix Workspace App must be configured to load the KandyDistant plugin*
The configuration file for the Citrix Workspace App can be found here:
`~/Library/Application\ Support/Citrix\ Receiver/Modules`

Edit the `module.ini` to add the necessary settings:
1. Open `/opt/Citrix/ICAClient/config/module.ini`
2. Locate the `[ICA 3.0]` section
3. Append the KandyDistant plugin to the `VirtualDriver` key. It should look similar to the following:
`VirtualDriver=Thinwire3.0, TWI, SmartCard, SSPI, TUI, KandyDistant.PlugIn`
4. Under the same section (`[ICA 3.0]`), add a key for our plugin and assign it the value of "On":
`KandyDistant.PlugIn=On`
5. Add a section for our plugin (and optionally set your custom executable path which defaults to `/usr/lib/rtc`):
```
[KandyDistant]
ExecutablePath = /your/path/
```

#### 3.2 Modifying Citrix Configuration
LogPath and LogLevel can be added and modified under the KandyDistant section.

ex:
```
[KandyDistant]
LogPath  = ~/Kandy/logs
LogLevel = debug
```

LogPath will default to `/var/log/kandy/`
LogLevel will default to `info`

Accepted log level values are:
- off
- critical
- error
- warn
- info
- debug
- trace


#### 3.3 KandyLib Configuration
KandyLib-specific configuration can be set and modified in your `kandy.ini` file which is expected to be found in `/setup` directory.

The `KandyDistant` section allows configuration flags that affect the browser container to be set.
Note that the legacy section, `RibbonRTC`, will still work but `KandyDistant` will take priority if both sections contain the same flag.

- CachePath: location where to store the application cache, defaults to: ~/Library/Application Support/Kandy/cache.
- CommandSwitch: Optional Command Switch arguments to be used with the browser container. Multiple command switches can be separated by a comma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.
- ExecutablePath: The absolute path to your execution path and configuration file
- CefLogLevel: The log level that CEF will use.
    - Accepted CEF log level values are:
        - off
        - critical
        - error
        - warn
        - info
        - debug
        - trace


#### 3.4 Sample (kandy.ini)
```
[KandyDistant]
CachePath=/tmp/kandy/cache
CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu
DebugPort=9222
CefLogLevel=trace
```

### 4. Before Running
Make sure that you have created appropriate directories for the KandyDistant log and the browser cache. These values should match your configuration of the Citrix `module.ini` file.
Default values are:
- `/var/log/kandy`
- `/tmp/kandy/cache`

Congratulations! You have built, signed, installed and configured the KandyDistant plugin for Citrix Workspace App on Elux!
