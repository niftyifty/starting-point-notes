# NMap
﷽ 	
## Useful resources: 
* [Cheatsheet](https://www.stationx.net/nmap-cheat-sheet/)
* `man nmap`
## Notes
* TCP Protocol: 
  * Starts w/ a SYN(chronisation) packet
  * Next is a SYN-ACK packet
  * Finished with an ACK packet.
    * **This is a three-way handshake.**

## Commands
* The `-T{number}` adjusts speed of the nmap scan. **For instance**:
  * `-T1` is slow, but you are careful and quiet.
  * `-T5` is very fast, but you might make more noise and miss more things.
  * Only use `-T5` when you dc about detection and you are in a trusted network. **It will trip firewalls.**
* Enable verbose mode by using the `-v` flag. **Nmap tells you what's happening step-by-step**.
  * You can increase amount of verbosity by adding `v`'s, eg. `-vvv` is extremely verbose and tells us EVERYTHING
* `-oX network-map.xml` and saves into an XML file for us to get a graphical view of all data from the scan.
  * This can be turned into a nice HTML file by running `xsltproc ./network-map.xml -o ./network-map.html`.
* `-F` flag uses top 100 ports only.

* `nmap -sn {target-subnet}` checks if hosts are alive. It's a "no ports scan" that scans the IP but no ports and is fast.
* From there, you can select an IP and run a default scan against it.
* The `-sV` flag allows us to view the specific versions of these services active, so we know what exploits to use. As we're enumerating deeper, it takes longer.
* The `-sC` flag uses default scripts from the `nmap scripting engine` against the target for adv recon.
* [SYN Scan]: The flag `-sS` in `sudo nmap -sS {ip} -p 443,8080` will scan ports 443 and 8080 of the target IP stealthily [-sS] by only sending a SYN packet.
  * This avoids tripping firewalls
* On the other hand, the `-sT` switch [TCP Control Scan] does the entire 3-way handshake
  * Slower, easier to detect but *doesn't require permissions* and you can make sure you have full connections.
* `-sU` can be used for a UDP scan
* The `-O` flag detects OSes
* The `-A` (Aggressive mode) flag is a combination of a few switches. Very informative but takes _ages_.

#### Obfuscation and avoiding detection
* Obfuscation helps you remain undetected. For example, `sudo nmap -sS -D {decoy-ip} {target-ip}` will send packets from both your IP and the decoy to throw blueteam off your tracks :)
* `nmap --spoof-mac 00:11:22:33:44:55 192.168.1.10` will spoof the MAC Addr. given.


#### Scripting
* Scripts can be used against targets to find vulnerabilities. Automation >>
* Example: `sudo nmap --script vuln {target-ip}` will attack the target with all Scripts in the [vuln] category on nmap scripting website and find exploits :)
* Applied examples:
  * `sudo nmap -p 443,8080 --script vuln {target-ip}`
    * Runs an nmap scan on the target IP's ports 443 and 8080 (web server) with the
  * `nmap -p 139,445 --script smb-os-discovery,smb-enum-shares,smb-enum-users {target-ip}`
    * SMB enumeration


## Commands

---

## 🔍 Basic Scanning

| Command                              | Description                             |
| ------------------------------------ | --------------------------------------- |
| `nmap <target>`                      | Basic scan (default top 1000 TCP ports) |
| `nmap -p- <target>`                  | Scan **all 65535 TCP ports**            |
| `nmap -F <target>`                   | Fast scan (top 100 ports)               |
| `nmap <target1> <target2> <target3>` | Scan multiple targets                   |
| `nmap -iL targets.txt`               | Scan list of targets from a file        |

---

## ⚡ Host Discovery

| Command             | Description                                                            |
| ------------------- | ---------------------------------------------------------------------- |
| `nmap -sn <target>` | Ping scan (host discovery only, no port scan)                          |
| `nmap -Pn <target>` | **No ping**, treat all hosts as online (useful for firewalled targets) |
| `nmap -n <target>`  | Don't resolve DNS (faster scan)                                        |

---

## 🚪 Port Scanning Techniques

| Command                       | Description                              |
| ----------------------------- | ---------------------------------------- |
| `nmap -sS <target>`           | **Stealth scan (SYN)** - common for OSCP |
| `nmap -sT <target>`           | TCP connect scan (less stealthy)         |
| `nmap -sU -p <port> <target>` | UDP scan (slower, fewer results)         |
| `nmap -p- -sS <target>`       | Full TCP port scan using stealth method  |

---

## 🔎 Service and Version Detection

| Command                           | Description                           |
| --------------------------------- | ------------------------------------- |
| `nmap -sV <target>`               | Detect **service versions**           |
| `nmap -p- -sV <target>`           | Full port scan with version detection |
| `nmap -sV --version-all <target>` | Try harder to guess all versions      |

---

## 🧠 OS Detection

| Command                           | Description                       |
| --------------------------------- | --------------------------------- |
| `nmap -O <target>`                | OS detection                      |
| `nmap -O --osscan-guess <target>` | Try to guess OS more aggressively |

---

## 🎯 Aggressive and All-in-One Scans

| Command                | Description                                           |
| ---------------------- | ----------------------------------------------------- |
| `nmap -A <target>`     | Aggressive scan: OS, version, script scan, traceroute |
| `nmap -A -p- <target>` | Full port scan + aggressive detection                 |
| `nmap -T4 -A <target>` | Faster aggressive scan with timing control            |

---

## 🧰 NSE (Nmap Scripting Engine)

| Command                                  | Description                         |
| ---------------------------------------- | ----------------------------------- |
| `nmap --script=default <target>`         | Run default scripts                 |
| `nmap --script vuln <target>`            | Run vulnerability detection scripts |
| `nmap --script http-title <target>`      | Get webpage titles                  |
| `nmap --script smb-enum-shares <target>` | Enumerate SMB shares                |

You can find more scripts in:

```bash
ls /usr/share/nmap/scripts/
```

---

## 🕓 Timing and Performance

| Command                | Description                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| `nmap -T0` to `-T5`    | Set timing from **paranoid (T0)** to **insane (T5)** — use `-T4` for OSCP |
| `nmap --min-rate 1000` | Send at least 1000 packets per second                                     |
| `nmap --max-retries 0` | Don’t retry (faster, but may miss ports)                                  |

---

## 💾 Output Options

| Command                 | Description                                            |
| ----------------------- | ------------------------------------------------------ |
| `nmap -oN output.txt`   | Normal output                                          |
| `nmap -oX output.xml`   | XML output                                             |
| `nmap -oG output.gnmap` | Greppable output                                       |
| `nmap -oA scan`         | Save **all formats** (scan.nmap, scan.xml, scan.gnmap) |

---

## 🧪 Evading Firewalls

| Command                          | Description                                 |
| -------------------------------- | ------------------------------------------- |
| `nmap -f <target>`               | Fragment packets                            |
| `nmap -D RND:10 <target>`        | Use decoy addresses                         |
| `nmap -S <spoofed-IP> <target>`  | Spoof source IP                             |
| `nmap --data-length 50 <target>` | Append junk data to probes                  |
| `nmap -Pn <target>`              | Skip host discovery (treat all hosts as up) |

---

## 🔁 Useful Combos

```bash
nmap -sS -sV -O -p- -T4 -oA fullscan <target>
```

🟢 Full stealth scan with service & OS detection, all ports, faster timing, and all output formats.

---

# 🧠 How to Use This with Ollama

If you want to use a local LLM like Ollama to **ask which command to use**, you can **pipe the cheatsheet into it** like this:

### Step 1: Save this cheatsheet to a file

```bash
nano nmap_cheatsheet.txt
```

(paste the above content)

### Step 2: Use a command like:

```bash
ollama run llama3 < nmap_cheatsheet.txt
```

Then ask:

> "Which command should I use to scan all ports and detect services on a host that might have ICMP blocked?"


