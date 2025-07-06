# John the Ripper
﷽
* Password hash-cracking utility.
## usage
### `zip` cracking

* first, convert the `zip` to a `hash` using the `zip2john` module:
  * `zip2john {file.zip} > hashes`

* then, crack it using `john`:
  * `john -wordlist={wordlist} hashes`

* once the password is cracked, use the `--show` option:
  * `john --show hashes`

* 
