# SSH - secure shell protocol
﷽
* provides a method for securely sending commands to a computer over an unsecured network.
## general usage
### upon obtaining an RSA key
* i have a RSA key, how may I use this to `ssh` into my victim?
* first, `touch id_rsa` to make the blank RSA key.
* now, `echo` / use `nvim` to put the key in this file.
* finally, set the right privileges for this key to be used by `ssh`:
  * `chmod 400 id_rsa`
* now we can `ssh` into the client:
  * `ssh -i id_rsa {user}@{ip}` 🎉

