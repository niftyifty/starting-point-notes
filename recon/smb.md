# SMB stuff
﷽

* SMB is a protocol used for file transfer.
* It stands for Server Message Block
* it runs on port 445.

## tools and usage

#### smbmap

* smbmap can scan and map shares
  * `cd` to `~/smbmap`, enter the `venv` and run the command `smbmap -H {ip}`.

#### smbclient

* to list shares on a network, run `smbclient -L //{ip}`
  * remember to check for common misconfigurations:
    * `smbclient -L //10.129.166.255 -U Administrator`, for example without the password.

* to connect to a specific share, run `smbclient //{ip}/{share}`, eg. `smbclient //10.129.3.185/backups`

#### `psexec.py`

* this script is part of the `impacket` collection, which is located in ~/impacket/ on my machine.

* `psexec` is a portable tool from Microsoft that allows you to run processes remotely.
* Remote access tool but instead you have a shell.

##### how it works

* A remote service is created by uploading a randomly-named executable on the `ADMIN$` share on the remote system.
* This is registered as a windows service.
* This results on an interactive shell being available on `TCP port 445`.
* `psexec.py` requires creds of a local Administrator (o+) because r/w to the `ADMIN$` share is required.
* Once authenticated fully, you will be dropped into a NT AUTHORITY\SYSTEM shell.

##### usage

* `cd` to `~/impacket/examples/` and run the command `psexec.py -h` for help.
* To connect to a server:
  * `psexec.py {username}@{target-ip}`
    * you will be prompted for the password.
* a shell should successfully be obtained.
