# Miscellaneous
﷽
## Name-Based v-hosting
* **Name-Based Virtual hosting** is a method for hosting multiple domain names (with separate handling of each name) on a single server. This allows one server to share its resources, such as memory and processor cycles, without requiring all the services to be used by the same hostname. The web server checks the domain name provided in the Host header field of the HTTP request and sends a response according to that.

* The `/etc/hosts` file is used to resolve a hostname into an IP address & thus we will need to add an entry in the `/etc/hosts` file for this domain to enable the browser to resolve the address for unika.htb . 

An example entry in the `/etc/hosts` file:
`echo "10.129.128.223 unika.htb" | sudo tee -a /etc/hosts`

## Ports and their information:
* https://www.speedguide.net/port.php?port=n where n is the port number eg. 23 for telnet.

## Information about webpages:
* `curl -v {website-name}` returns amazing info about a website.




## Finding files
To find all files in the current directory and its subdirectories that have nmap in the filename, use:

bash
Copy
Edit
find . -type f -iname '*nmap*'
🔍 Explanation:
. → current directory

-type f → files only

-iname → case-insensitive name match

'*nmap*' → matches anything with nmap in the name


