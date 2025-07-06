# Redis
﷽
* **Redis (REmote DIctionary Server)** is an open-source advanced NoSQL key-value data store used as a database, cache, and message broker. The data is stored in a dictionary format having key-value pairs. It is typically used for short term storage of data that needs fast retrieval. ***Data is backed up to hard drives to provide consistency.***
* It is a **server-side** software.

## Usage
* Note that `nc` may also be used.
  * However, the `redis-cli` tool is better and more suited.
* Get help:
  * `redis-cli --help`
* To connect to a server, specify a hostname with the `-h` flag:
  * `redis-cli -h {target-ip}`
### Upon connection
* Upon connection, many things may be done.
* A common enumeration command is `info`, which returns information about the server.
* The `keyspace` section in `info` provides statistics on the main dictionary of each database.
* To select a database:
  * `select {db-name}`
* From there, we can list all keys:
  * `keys *`
* We can view the value of a key by using the `get` command:
  * `get flag`
  ~ $ "0eEfn3r8sjka9n"
Simple :)


