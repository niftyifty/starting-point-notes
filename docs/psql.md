# PostGreSQL
﷽
## usage

* to connect to a server:
  * `psql -h {hostname} -U {username} -p {port}`
  * eg. `psql -h localhost -U andrew -p 1234`
* you will be prompted for a password, which after entering:

### upon connection

* to list existing databases, use
  * `\1`, which is short for `\list`

* to enter a database,
  * `\c {db-name}`, short for `\connect`

* list the DB's tables:
  * `\dt`

* dump contents using the conventional
  * `SELECT * FROM {name}`

* 
