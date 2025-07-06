# Tunnelling
﷽

* Something that one can use to access resources that are only available internally.
* Tunneling in computer networking is a method of sending data from one network to another by encapsulating it inside packets of a different protocol. This allows data to pass securely or privately through incompatible or public networks.
* Common protocols include `SSH (Secure Shell Protocol)`.

## How Tunnelling works (SSH)

* [Ref. video](https://www.youtube.com/watch?v=AtuAdk4MwWw)

* The client authenticates to the server for the connection to succeed.
* After the connection is established, we have a valid `SSH` session and we (the client) can interact with the server through a shell.

* The main thing to point out is that the data that gets transported through this session can be of any type. 
* This is what allows us to create `SSH` tunnels within a valid `SSH` shell.

## Types of tunnelling
### `Local Port Forwarding`

* What it does: Forwards traffic from your local machine → to a remote server.
* Use case: Accessing a remote service (like a database or website) that’s behind a firewall.

* Example: You can't access a remote database directly, but you SSH into the server and forward the database port to your laptop.

* Command example:
  * `ssh -L 8080:internal.server.com:80 user@sshserver.com`
* Now you can access http://localhost:8080, and it'll connect to internal.server.com:80 via the SSH server.

* ***Basically, suppose port 3389 was blocked on a school computer so I couldn't use remote desktop.***
  * ***I could forward the data from that port to an unblocked port like 8181 instead so data was forwarded, but just on a different port.***

## Ah, got it! You're talking about the **types of SSH tunneling** — local, remote, and dynamic tunneling. Here’s a **simple breakdown** of each:

---

### 🟩 1. **Local Port Forwarding**

* **What it does:** Forwards traffic **from your local machine → to a remote server**.

* **Use case:** Accessing a remote service (like a database or website) that’s behind a firewall.

* **Example:**
  You can't access a remote database directly, but you SSH into the server and forward the database port to your laptop.

* **Command example:**

  ```bash
  ssh -L 8080:internal.server.com:80 user@sshserver.com
  ```

  Now you can access `http://localhost:8080`, and it'll connect to `internal.server.com:80` via the SSH server.

* **Analogy:** Like poking a straw through your SSH tunnel so **you can suck remote data through your local port**.

---

### 🟦 2. **Remote Port Forwarding**

* **What it does:** Forwards traffic **from a remote machine → to your local machine**.
* **Use case:** Allowing someone to access a service running on your machine via an SSH server.
* **Example:**
  You're running a web app on your laptop (port 5000), and want someone on the internet to access it through your SSH server.
* **Command example:**
  `ssh -R 9000:localhost:5000 user@sshserver.com`
Now, visiting `sshserver.com:9000` shows your app running locally.
* **Analogy:** Like letting someone use your SSH tunnel to **reach into your local machine**.

---

### 🟨 3. **Dynamic Port Forwarding**
* **What it does:** Turns your SSH client into a **SOCKS proxy**.
* **Use case:** Routing web traffic through a remote server (like using a VPN or bypassing firewalls).
* **Example:**
  You want your browser to route traffic through an SSH server.
* **Command example:**
  ```bash
  ssh -D 1080 user@sshserver.com
  ```
  ```

  ```
  Set your browser to use `localhost:1080` as a SOCKS proxy.
* **Analogy:** Like opening a **smart tunnel** where your SSH connection acts as a **proxy server**, deciding where each request goes.
### 🧠 Summary Table:

| Type    | Traffic Direction                | Use Case                        | Port Example |
| ------- | -------------------------------- | ------------------------------- | ------------ |
| Local   | Local → Remote                   | Access remote services securely | `-L`         |
| Remote  | Remote → Local                   | Share local services            | `-R`         |
| Dynamic | Local ⇄ Remote (via SOCKS proxy) | Browse web via SSH (like VPN)   | `-D`         |


## Usage

* Crucial command to check socket statistics:
  * `ss -tl(n)`
    * `t`: Display only TCP sockets
    * `-l`: Display only listening sockets
    * (don't have to use, but) `-n`: Don't try resolve service name
* This command is basically used to check open ports on the local computer that `nmap` can't find as they're local.

#### Example with Local Port Forwarding SSH

* The command `ssh -L 1234:localhost:22 user@remote.example.com` will:
  * Forward traffic from the local port `1234` on this machine to the remote server `remote.example.com`'s `localhost` interface on port 22.
  * When running this command, SSH establishes a connection to the remote SSH server.
  * It will listen for incoming connections on the local port `1234`.
  * When a client connects to the local port, the SSH client will forward the connection to the remote server on port `22`. 
  * This allows the local client to access services on the remote server as if they were running on the local machine.

  * So, when this command in specific is ran, the SSH client will ***connect to the remote SSH server and listen for incoming connections on `port 1234`.***
  * ***When a client connects to the local port, the SSH client will forward the connection to the remote server (us) on port 22.***
  * This allows the local client to access services on the remote server as if they were running on the local machine.
  * In the scenario we are currently facing, we want to forward traffic from any given local port, for instance 1234 , to the port on which PostgreSQL is listening, namely 5432 , on the remote server. We therefore specify port 1234 to the left of localhost , and 5432 to the right, indicating the target port.

* We can see this socket running on **our port `1234`**, which ***we can now direct traffic that we want forwarded to port 5432 on the target machine.***
  * Use this command on the local machine to see this: 
    * `ss -tlpn`, where `-p` means ____.

#### Example with dynamic port forwarding SSH

* Unlike local port forwarding and remote port forwarding, which use a specific local and remote port (earlier we used 1234 and 5432 , for instance), dynamic port forwarding uses a single local port and dynamically assigns remote ports for each connection.

* ik i didn't really get that, BUT:

### `ProxyChains`

*  proxychains can be used to tunnel a connection through multiple proxies
* good for anonymity on the internet.

* ***Configurable through ``/etc/proxychains4.conf``

* In our current use case, of dynamic port forwarding, we should configure it to:

1. Ensure that strict_chain is not commented out; ( dynamic_chain and random_chain should be commented out)
2. At the very bottom of the file, under `[ProxyList]` , we specify the `socks5` (or `socks4`) host and port that we used for our tunnel.

* So, in our case it would look something like this:

```
<SNIP>
[ProxyList]
# add proxy here ...
# meanwile
# defaults set to "tor"
#socks4 127.0.0.1 9050
socks5 127.0.0.1 1234
```

We can now connect to the `PostgreSQL` service as if we were on the machine!
* `proxychains psql -U christine -h localhost -p 5432`

> [!NOTE]
> ProxyChains can release a lot of output, but it's just its verbosity.


