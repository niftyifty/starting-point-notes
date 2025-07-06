# AWSCLI
﷽
* Can be used to interact with s3 buckets.
## usage

* first, configure it with:
  * `aws configure`

* you can list all s3 buckets on a server by using the `ls` command:
  * `aws --endpoint={server-name} s3 ls`
  * eg. `aws --endpoint=http://s3.thetoppers.htb s3 ls`

* the `ls` command can also be used to list objects and common prefixes unter the host, **eg.**):
  * `aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb`

* We can also copy files between our computer and s3:
  * `aws --endpoint={server-name} s3 cp {file-name} {server-name}`


