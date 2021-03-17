# @kandy-io/kandy-distant-vdi

## Kandy Distant Driver for VDI Windows

This driver adds support for the [Citrix Workspace App](https://docs.citrix.com/en-us/citrix-workspace-app.html) on Windows for use on Desktops.

### Requirements

Windows 10 64 bit.
Dual Core CPU with 4 GB RAM recommended.

### Installation

There is no installer provided to install the driver, developers needs to create an installer for their customers to use. The driver files need to be installed in the Citrix ICA program folder and the program files in a folder of their choice (refered below as the Executable Path). Then The Windows Registry needs to be updated to load the Driver and point to the program folder. We provide a PowerShell script as a reference on how these steps can be acheived.

The provided ZIP Archive contains the program and driver folders, as well as the version file and the PowerShell script.

#### PowerShell script

The install.ps1 script is given as an example on how to install the files, and will setup the application with some defaults path. The Script needs to be run as an administrator and will install the program into C:\Program Files\Kandy. 

#### Files

Copy the files contained in the different folders to the following locations

driver/* -> C:\Program Files (x86)\Citrix\ICA Client\\

program/* -> *EXECUTABLE_PATH_HERE* (ex: C:\Program Files\Kandy\\)

#### Registry

In order for the Driver to be loaded by The Cirtirx Workspace App it needs to be added to the Windows Registry
1. Locate the VirtualDriverEx string REG_SZ value in the *HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Citrix\ICA Client\Engine\Configuration\Advanced\Modules\ICA 3.0* key. Append the *KandyDistant* to the end of this line.
2. Under the *HKLM:\Software\WOW6432Node\Citrix\ICA Client\Engine\Configuration\Advanced\Modules* key, create a new key named *KandyDistant*.
3. Under *KandyDistant*, add the following string REG_SZ values:
 - DriverName = Unsupported
 - DriverNameWin16 = Unsupported
 - DriverNameWin32 = KANDY_DISTANT.DLL
 - ExecutablePath = *EXECUTABLE_PATH_HERE* (ex: C:\Program Files\Kandy)

### Configuration

The configuration is loaded from config.ini and from the registry.

LogPath and LogLevel can be added as string REG_SZ value to the registry under the KandyDistant key created above.

ex:
- LogPath = C:\tmp
- LogLevel = debug

LogPath will default to %AppData%\Kandy\DistantVDI\Log, and must be an absolute path witout spaces
LogLevel 

#### RibbonRTC (config.ini)

This section allow to set different configuration flags that affect the browser container.

- CachePath: location where to store the application cache. defaults to: %AppData%\Kandy\DistantVDI\Cache
- CommandSwitch: Command Switch arguments to be used with the browser container. Multiple connad switch can be separated by a coma.
- DebugPort: Debug port to be used for development. If no port is provided the debug port is disabled.

#### Sample (config.ini)

[RibbonRTC]

CachePath=c:\tmp\cache

CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu

DebugPort=9222