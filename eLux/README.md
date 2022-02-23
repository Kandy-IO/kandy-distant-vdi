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

#### 3.1 KandyDistant Configuration
KandyDistant-specific configuration can be set and modified in your `kandy.ini` file which is expected to be found in `/setup` directory.

The `KandyDistant` section allows configuration flags that affect the browser container to be set.
Note that the legacy section, `RibbonRTC`, will still work but `KandyDistant` will take priority if both sections contain the same flag.

- CachePath: location where to store the application cache, defaults to: `/tmp/kandy/cache`.
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
- LogLevel: The log level that KandyDistant will use. Defaults to `info`.
    - Accepted log level values are:
        - off
        - critical
        - error
        - warn
        - info
        - debug
        - trace

#### 3.2 Sample (kandy.ini)
```
[KandyDistant]
CachePath=/tmp/kandy/cache
CommandSwitch=ignore-certificate-errors,disable-extensions,disable-gpu
DebugPort=9222
CefLogLevel=trace
LogLevel=debug
```

### 4. Logs
The logs can be found at `/var/log/kandy/`.


### 5. Known Issues / Limitations
#### Issues
- Internal VDI error when removing device while application is running. `KAJ-1006`

#### Unreleased Fixes
- Window can suddenly not be visible when opening and closing sessions multiple times. `KAJ-1007`
- Quickly closing a session right after opening it will cause the VDI solution to freeze. `KAJ-1009`

