# SUID (Set owner User ID)

* ***look for `setuid`***

﷽
* a file with SUID always executes as the user who **owns** the file, regardless of the user passing the command.
* if the file owner doesn't have `execute` permissions, use an uppercase `S` here.

## usage
### scenario #1: the binary is owned by `root` and can be executed as `root` since it has SUID set.

* run the file and see what exploits it has. in my case there was a `cat` exploit, so hop over to `cat-exploit.md` to see the exploit in full. gl :)

