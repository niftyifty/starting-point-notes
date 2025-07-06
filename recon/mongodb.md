# MongoDB
﷽
* A utility for databases. 
* Runs on ***Port 27017***
## Usage
* Then, connect to a server by running
  * `mongosh mongodb://{target_IP}:27017`
## In-shell Usage
* To get help:
  * `help`
* List databases on the server:
  * `show dbs;`
* Select a database by using:
  * `select {db-name};`
* Then, show collections by:
  * `show collections;`
* You can dump the contents in a collection by using:
  * `db.{collection-name}.find()`
  eg. `db.flag.find()`

## Password extraction
* first, check if `mongodb` is on the target:
  * `ps aux | grep mongo`
* print from a db:
  * `mongosh --port 27117 {db-name} --eval "db.admin.find().forEach(print.json);"`

