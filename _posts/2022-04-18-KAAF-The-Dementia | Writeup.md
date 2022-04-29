layout: post
title:  KAAF : The Dementia
categories: CTF
author: ThelastVvV
date: '2022-04-18 05:00:53 +0000'
tags:
  - CTF
  - CyberSecurity
  - TryHackMe
  - hackthebox
published: true
---
### Tablet of Content:

- [Task 1: Reconnaissance & Scanning](#task1)
- [Task 2 : Boot To Root](#task2)
<!-- toc -->

## KAAF : The Dementia
## The easiest CTF for beginners



>  Note*:Summary writeup some steps were skipped ...




# Task 1: Reconnaissance & Scanning

### Question #1: 
```sh
gobuster dir -u http://10.0.2.5 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
```
Results :
```sh
/ftp                  (Status: 301) [Size: 302] [--> http://10.0.2.5/ftp/]
```
Manual checking we get
```sh
/ftp/upload/
```
### Question #2:
```sh
nmap -T4 -A -v -Pn  10.0.2.5
```
Results:
```sh
ORT     STATE SERVICE       VERSION

21/tcp   open  ftp           vsftpd 2.0.8 or later

| ftp-syst: 

|   STAT: 

| FTP server status:

|      Connected to ::ffff:10.0.2.4

|      Logged in as ftp

|      TYPE: ASCII

|      No session bandwidth limit

|      Session timeout in seconds is 300

|      Control connection is plain text

|      Data connections will be plain text

|      At session startup, client count was 3

|      vsFTPd 3.0.3 - secure, fast, stable

|_End of status

| ftp-anon: Anonymous FTP login allowed (FTP code 230)

| drwxrwxrwx    2 33       33           4096 Apr 20 18:36 upload [NSE: writeable]

|_-rw-r--r--    1 33       33             49 Mar 29 22:51 vvv.txt

22/tcp   open  ssh           OpenSSH 8.2p1 Ubuntu 4ubuntu0.4 (Ubuntu Linux; protocol 2.0)

| ssh-hostkey: 

|   3072 e7:26:d1:3f:6e:7f:cb:f4:34:98:98:33:57:86:1b:8e (RSA)

|   256 38:6a:fc:16:b1:67:f6:ba:96:88:db:09:8e:6a:a8:83 (ECDSA)

|_  256 92:67:9d:d1:c3:0d:1d:b0:84:df:d6:44:7f:6b:c9:60 (ED25519)

80/tcp   open  http          Apache httpd 2.4.41 ((Ubuntu))

| http-methods: 

|_  Supported Methods: POST OPTIONS HEAD GET

|_http-title: Site doesn't have a title (text/html).

|_http-server-header: Apache/2.4.41 (Ubuntu)

3389/tcp open  ms-wbt-server xrdp

Service Info: Host: Fahd; OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

Conclusion : ftp misconfiguration that allows anon login

Answer:ftp

### Question #3:

Answer:21
# Task 2 : Boot To Root
### Question #1:
Answer:anonymous:anonymous

### Question #2:
Answer: vvv.txt

Question #3:

Answer: www-data

### Question #4:
Check the premission of the above user ,from www-data user  we need to have access with root privileges and capturing flags in user and root .  as we find earlier that we have misconfiguration in sudeors that lead that www-data can run env binary program using sudo without root password

More details:

https://gtfobins.github.io/gtfobins/env/

Trick: To get user flag we need to get the root access first

User flag in 
```sh
/home/kaaf/
```
### Question #5:
Root flag :
```sh
/root/root.txt
```
