# Web App Methodology
﷽
* Methodology for Web App exploitation
## Methodology
* firstly, scan the website with `nmap` to see what ports are open, etc.
* then, use gobuster to try dir/vhost scan for hidden directories.
* then, try checking if the files can be listed (ie),
  * if in `example.com/login/login.php`, try accessing 
  * `example.com/login`

