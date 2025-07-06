# RSync
﷽
* A utility for copying files between servers.

### Stages of connection

1. rsync establishes a connection to the remote host and spawns another rsync receiver process.
2. The sender and receiver processes compare what files have changed.
3. What has changed gets updated on the remote host.

## Usage

