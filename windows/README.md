# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI Windows

This driver adds support for [Citrix Workspace App for Windows](https://docs.citrix.com/en-us/citrix-workspace-app-for-windows.html).

### 1. Requirements

Windows 10 64 bit (Home Edition not supported by Citrix)

Citrix Workspace App for Windows 2012+ (tested on 2102 in release 1.0.0)

Dual Core CPU with 4 GB RAM recommended.

### 2. Installation

There is no installer provided to install the driver, developers needs to create an installer for their customers to use. The driver files need to be installed in the Citrix ICA program folder and the program files in a folder of their choice (referred below as the Executable Path). Then the Windows Registry needs to be updated to load the driver and point to the program folder. We provide a PowerShell script as a reference on how these steps can be acheived.

The provided ZIP archive contains the program and driver folders, as well as the version file and the PowerShell script.

#### PowerShell script

The install.ps1 script is given as an example on how to install the files, and will setup the application with some defaults path. The script needs to be run as an administrator and will install the program into C:\Program Files\Kandy.

#### Files

Copy the files contained in the different folders to the following locations

driver/* -> C:\Program Files (x86)\Citrix\ICA Client\\

program/* -> *EXECUTABLE_PATH_HERE* (ex: C:\Program Files\Kandy\\)

#### Registry

In order for the Driver to be loaded by the Citrix Workspace App it needs to be added to the Windows Registry
1. Locate the VirtualDriverEx string REG_SZ value in the *HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Citrix\ICA Client\Engine\Configuration\Advanced\Modules\ICA 3.0* key. This setting is a comma separated list. Set the value to 'KandyDistant' if the value is empty or append ',KandyDistant' if there is already a value. ie: 'VirtualDriverEx = KandyDistant' or 'VirtualDriverEx = DriverX,KandyDistant'.
2. Under the *HKLM\Software\WOW6432Node\Citrix\ICA Client\Engine\Configuration\Advanced\Modules* key, create a new key named *KandyDistant*.
3. Under *KandyDistant*, add the following string REG_SZ values:
 - DriverName = Unsupported
 - DriverNameWin16 = Unsupported
 - DriverNameWin32 = KANDY_DISTANT.DLL
 - ExecutablePath = *EXECUTABLE_PATH_HERE* (ex: C:\Program Files\Kandy)

### 3. Configuration

The configuration is loaded partially from config.ini and partially from the registry.

#### Windows Registry

LogPath and LogLevel can be added as string REG_SZ value to the registry under the KandyDistant key created above.

ex:
- LogPath = C:\tmp
- LogLevel = debug

LogPath will default to %AppData%\Kandy\DistantVDI\Log, and must be an absolute path without spaces.
LogLevel default to info and can be configured with off, critical, error, warn, info, debug and trace

#### KandyDistant (config.ini)

This section allows configuration flags that affect the browser container to be set.

- CachePath: location where to store the application cache, defaults to: %AppData%\Kandy\DistantVDI\Cache.
- CommandSwitch: Optional Command Switch arguments to be used with the browser container. Multiple command switches can be separated by a comma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.
- SessionOverwrite: When enabled, the Kandy Distant Driver handles Session Start requests by creating a new session which overwrites any existing session. Accepted values are: `true`, `false` (default)
- CefLogLevel: Log level used by CEF. Defaults to `info`. Other available choices are `trace`, `debug`, `info`, `warn`, `error`, `critical`, or `off`. `debug` option will display verbose level 1 CEF logs.
- VerboseLevel: Number flag indicating how verbose the CEF logs will be.
- VerboseModules: Number flag indicating how verbose CEF logs will be on a per module basis. Where the modules are chromium modules and can be found here https://source.chromium.org/chromium/chromium/src. Number used can range from `1` to `3` and `-3` for filtering out modules.

#### Sample (config.ini)
```
[KandyDistant]
CachePath=c:\tmp\cache
CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu
DebugPort=9222
SessionOverwrite=false
CefLogLevel=debug
VerboseLevel=1
VerboseModules=*webrtc*=1,*=-3
```
In this example, VerboseModules will show verbose level 1 webrtc logs and will filter out all other modules.

### 4. Logs
By default, the logs can be found at `<user>/AppData/Roaming/Kandy/DistantVDI/Logs`.

#### 4.1 Log Rotation
Each time the VDI driver is run, log files with the following format will be created:
- `distant-<pid>.log` - The vdi driver logs.
- `browser_console-<pid>.log` - The browser process CEF logs.

When the VDI Driver is run, log files that are 7 or more days old will be deleted.

## 5. Sleep & Disconnect
CWA (Citrix Workspace App) handles computer sleep and network disconnects somewhat differently on each OS. This has some impact on Distant and your Distant sessions. It is important that your application can handle these scenarios. Please refer to the subsections for more information.

### 5.1 Sleep
When waking from a short sleep (less than approximately 3 minutes) the CWA will resume and your original Distant session will be available.

When waking from a long sleep (more than approximately 3 minutes) :
 - The CWA may exit in which case your Distant session will be closed.
 - The CWA may exit and restart in which case your Distant session may be reloaded, or closed.

### 5.2 Disconnect
When reconnected after being disconnected for a duration of under 3 minutes, the CWA will resume and your original Distant session will be available.

When reconnected after being disconnected for a duration of more than 3 minutes, the CWA will resume and your Distant session may be reloaded.

When still disconnected for more than 5 minutes, the CWA your Distant session will be closed. The user will need to open a new Citrix connection and create a new session once they have an internet connection.

### 6. Known Issues / Limitations
