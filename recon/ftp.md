# FTP
* FTP is a protocol on port 21 for transferring files.
* SFTP is secure FTP and is on port 22.

## Notes

* A typical misconfiguration for FTP allows an `anonymous` account to access the service like any other user, without any password. [(username `anonymous` obviously)]


## Usage - Host OS

  * For help, type `ftp -?`

* To connect to a FTP client:
    * `ftp {target-ip}`
      * Then enter username and password when prompted. (`anonymous` is a good one)

## Usage - FTP shell

* To get help, use `help`.
* All commands are in the commands section below.

* Use `dir` get a list of files.
* `get` downloads a copy of that file to the folder you started the tool in.


## Commands

!               edit            lpage           nlist           rcvbuf          struct
$               epsv            lpwd            nmap            recv            sunique
account         epsv4           ls              ntrans          reget           system
append          epsv6           macdef          open            remopts         tenex
ascii           exit            mdelete         page            rename          throttle
bell            features        mdir            passive         reset           trace
binary          fget            mget            pdir            restart         type
bye             form            mkdir           pls             rhelp           umask
case            ftp             mls             pmlsd           rmdir           unset
cd              gate            mlsd            preserve        rstatus         usage
cdup            get             mlst            progress        runique         user
chmod           glob            mode            prompt          send            verbose
close           hash            modtime         proxy           sendport        xferbuf
cr              help            more            put             set             ?
debug           idle            mput            pwd             site
delete          image           mreget          quit            size
dir             lcd             msend           quote           sndbuf
disconnect      less            newer           rate            status

