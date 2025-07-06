# Password Cracking
﷽
* Guide on Password Cracking.
* Hashes are **one-way**
## Hash replacement
* If we find a hash assigned to a variable, we can replace the variable with our own hash, which is for one we know the password.
* There will be an identifier at the start of the hash, such as `$6$` which tells us it is SHA-512 in this case.
Replace it with another hash:
  * `mkpasswd -m sha-512 password`, where
    * `sha-512` is the cryptographic algorithm, and
    * `password` is the password.
