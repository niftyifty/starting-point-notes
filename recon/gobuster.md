# GoBuster
﷽
* A tool that can brute-force directories and files of a website like `login.example.com` or `example.com/login`.
* ***It is NOISY as it is a BF tool.***

## Usage
* GoBuster has many useful flags and options..
### `dir`
  * Using the `dir` option specifies we are directory hunting.
  * It is used to find directories such as /admin, /login, etc..
   * eg. `gobuster dir --url {url} --wordlist {wordlist.txt} -x php,html`
  * The `--url` flag specifies the URL we are to use.
  * The `--wordlist` flag specifies the wordlist we are to use [.txt]
  * The `-x` flag specifies what filetypes to look for in order to only get the useful ones we want.
### vhost
* The `vhost` option is useful for finding subdomains.
* eg. `gobuster vhost -u example.com -w wordlist.txt`
* This would look for subdomains, eg. the `asim` in `asim.niftyifty.com`


