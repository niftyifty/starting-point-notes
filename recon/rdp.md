# RDP - Remote Desktop Protocol
﷽
* A Protocol for connecting to computers remotely.

## CLI Usage
* To install:
  * `brew install freerdp`
### Connection
* eg. `xfreerdp /v:{target-ip} /cert:ignore /u:Administrator`, where:
  * `/v:` specifies target IP,
  * `/cert:` specifies that all sec. certs shouldn't be used, and
  * `/u:` specifies the username to use (in our case `Administrator`)

### In-shell usage

