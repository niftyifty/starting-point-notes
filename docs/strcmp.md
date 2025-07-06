# `strcmp()` vuln
﷽
* Vulnerability in the `strcmp()` function, a function that is used to compare two strings in PHP.
## guide
* sometimes, the `strcmp()` function is used to check if the username and password match the correct ones. it passes 0 when correct.
* however, this function is insecure: 
  * This is due to the fact that if strcmp is given an empty array to compare against the stored password, it will return NULL . In PHP the (double equals) operator only checks the value of a variable for equality, and the value of NULL is equal to 0 . The correct way to write this would be with the === operator which checks both value and type. These are prominently known as "Type Juggling bugs" and a detailed video explanation on this can be found [here.](https://www.youtube.com/watch?v=idC5SAsKhlE)

* In PHP, variables can be easily converted into arrays if we add [] in front of them. For example:
  * `$username = "Admin"
  $username[] = "Admin"`

* adding `[]` to the variable makes it an array. this means that ***strcmp will compare the array instead of a string***.
  * `if (strcmp($username , $_POST['username']) == 0) {
     if (strcmp($password, $_POST['password']) == 0) {`
In the above code we see that if the comparison succeeds and returns 0 , the login is successful. If we convert those variables into empty arrays ( $username[] & $password[] ), the comparison will return NULL , and NULL == 0 will return true, causing the login to be successful.
### remember, ***`NULL` = 0 = TRUE***
---
## doing the exploit
* capture the login request in burp, and edit the request so that:
`username[]=admin&password[]=pass`, instead of the `username=admin&password=pass` that was before.
* as both are now arrays, `strcmp` will evaluate to `true`, and login should be successful :)

