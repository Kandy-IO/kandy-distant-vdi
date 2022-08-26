# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI eLux

This driver adds support for [Citrix Workspace App for Linux](https://docs.citrix.com/en-us/citrix-workspace-app-for-linux.html) on [eLux OS](https://www.unicon-software.com/products/elux/) for use on thin clients.

### 1. eLux Package Signature

Validating package signatures requires the following certificates from [Sectigo's main page](https://support.sectigo.com/articles/Knowledge/Sectigo-Intermediate-Certificates):

Root Certificate:<br>
[AAA Certificate Services](https://comodoca.my.salesforce.com/sfc/p/1N000002Ljih/a/3l000000sYVG/4l82xrBbMv8Ndh.SBoUvQs0BjYk_pJlb4Sa92KfrsxY)

Intermediate Certificates:<br>
[Sectigo Public Code Signing CA R36](https://comodoca.my.salesforce.com/sfc/p/#1N000002Ljih/a/3l000000oAhy/QCCby12C7cYo50nNyic6AuG1KFcwe1rDn1EknfTaUzY)<br>
[SectigoPublicCodeSigningRootR46_AAA [ Cross Signed ]](https://comodoca.my.salesforce.com/sfc/p/1N000002Ljih/a/3l000000sYVB/t5kHfAZUjSL8NyXDwAQ3OhmfoTNSOnWgpnTmksjVyJc)

### 2. Browser Container Certificates

eLux 6.9 provides certificate management directly in the OS for our browser container. If there is a need to use custom certificates for reaching https websites in the browser container please ignore the Certificate Configuration below and put the certificate in the /setup/cacerts/browser folder as mentioned in the eLux [Documentation](https://www.unicon-software.com/udocs/en/#admin_guides/scout_enterprise/app_definition/browser/browser_config.htm?Highlight=cacert).

### 3. Configuration

#### 3.1 KandyDistant Configuration
KandyDistant-specific configuration can be set and modified in your `kandy.ini` file which is expected to be found in `/setup` directory.

The `KandyDistant` section allows configuration flags that affect the browser container to be set.
Note that the legacy section, `RibbonRTC`, will still work but `KandyDistant` will take priority if both sections contain the same flag.

- CachePath: location where to store the application cache, defaults to: `/tmp/kandy/cache`.
- CommandSwitch: Optional Command Switch arguments to be used with the browser container. Multiple command switches can be separated by a comma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.
- ExecutablePath: The absolute path to your execution path and configuration file
- SessionOverwrite: When enabled, the Kandy Distant Driver handles Session Start requests by creating a new session which overwrites any existing session. Accepted values are: `true`, `false` (default)
- CefLogLevel: The log level that CEF will use. Defaults to `info`. Other available choices are `trace`, `debug`, `info`, `warn`, `error`, `critical`, or `off`. `debug` option will display verbose level 1 CEF logs.
- VerboseLevel: Number flag indicating how verbose the CEF logs will be. Only supports `1`.
- VerboseModules: Number flag indicating how verbose CEF logs will be on a per module basis. Where the modules are chromium modules and can be found here https://source.chromium.org/chromium/chromium/src. Number used can range from `1` to `3` and `-3` for filtering out modules. For this to work, VerboseLevel must be set to `1`.
- DebugUrlEnabled: When enabled, a new session can be started with the debug url `http://locahost:DebugPort` or a `chrome://` url. Whith thse special urls the session will be opened in a new window outside of the Citrix window. ex: Specifying a new session with the following url `chrome://version` will open the chromium version information. Accepted values are: `true`, `false` (default)

#### 3.2 Sample (kandy.ini)

```
[KandyDistant]
CachePath=/tmp/kandy/cache
CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu
DebugPort=9222
LogLevel=debug
SessionOverwrite=false
CefLogLevel=debug
VerboseLevel=1
VerboseModules=*webrtc*=1,*=-3
DebugUrlEnabled=true
```
In this example, VerboseModules will show verbose level 1 webrtc logs and will filter out all other modules.

### 4. Logs
By default, the logs can be found at `/var/log/kandy/`.

#### 4.1 Log Rotation
Each time the VDI driver is run, log files with the following format will be created:
- `distant-<pid>.log` - The vdi driver logs.
- `browser_console-<pid>.log` - The browser process CEF logs.

The maximum number of distant log files is 5.
When the VDI Driver is run and there are 5 or more distant log files, they will be rotated.

### 5. Known Issues / Limitations
