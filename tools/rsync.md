# RSync
﷽
* A file copying tool.
* Runs on port `873`.
## Usage

* If a username is not specified, an anonymous authentication will take place:
  * `rsync --list-only {target-ip}::`
    * Judging by the output, you can further enumerate;
      * `rsync --list-only {target-ip}::{share-name}`

* To copy and paste between the host and ourselves, we can:
  * `rsync {target-ip}::{share-name}/{file-name} {destination-file-name}`
  * eg. `rsync {target_IP}::public/flag.txt flag.txt`

