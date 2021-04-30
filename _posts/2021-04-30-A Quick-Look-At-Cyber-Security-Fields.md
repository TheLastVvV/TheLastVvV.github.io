---
layout: post
title: A Quick Look At Cyber Security Fields 
categories: Cyber Security
author: ThelastVvV
date: '2021-04-30 05:00:53 +0000'
tags:
  - blog
  - CyberSecurity
  - science
published: true
---

### Table of contents

- [Introduction](#introduction)
- [Web security](#Web-security)
  - [SQL injection ](#SQL-injection)
  - [Cross site-scripting ](#Cross-site-scripting)
  - [ Security Misconfiguration ](#Security-Misconfiguration)
 - [Software Security](#Software-Security)
   - [Buffer Overflow ](#Buffer-Overflow )
  - [IP Security  ](#IP-Security  )
  - [Email Security  ](#Email-Security  )
  - [ Conclusion  ](#Conclusion  )
<!-- toc -->
 



## Introduction
Today during these harsh times of covid-19 we believe that cyber security is important now more than ever as we can see internet is part of our daily life, and that why everyone should understand and comprehend all the things that come with it from the basics to security. 
Cyber security is combination of practice, strategies and policies that aim to protect systems, networks and data from malicious attacks and best way to protect these things is educate internet users to understand the attacks and risks and how take the necessary measures to defends their systems and electronic assets and in this report the users will have quick look at cyber security fields as part of our contribution to help making the internet a safe and secure place. 

## Web security
Web security field is incredibly famous branch of cyber security as we can see most internet users either own or visit websites and it's important to know how threat actors attack these websites and how to protect them, this why we can showcase some famous OWASP top ten web application security vulnerabilities: SQL injection, Cross-site scripting, and Broken Access Control. 

 ### SQL injection
 
 SQL Injection: the threat attacker can inject SQL commands to manipulate or expose hidden data of the database and Theres many types of  SQL injection.  
- Attack : 

As we cans see below, we have a vulnerable website   that we will try SQL injection on it  
![alt text](https://thelastvvv.github.io/images/posts/5/sql_1.png "sql1")
The ways to check is by add a “ ‘ “ apostrophe at end of the id  ?id=1’ 
As we can see sometimes  you have some kind of error that indicates that there is a SQL error or just missing and broken things in the page 
![alt text](https://thelastvvv.github.io/images/posts/5/sql_2.png "sql2")
We keep testing until the page return to normal states in this case in id 4 which means that there's 4 columns in the database. Now we preform onion injection to check vulnerable columns in this case we have 3 and 4 that we can manipulate and get the data we want  
![alt text](https://thelastvvv.github.io/images/posts/5/sql_3.png "sql3")
A Simple SQL commands like database()  in vulnerable columns and we retrieved the database name 
![alt text](https://thelastvvv.github.io/images/posts/5/sql_4.png "sql4")
Now we will retrieve username and password from the users table  using the vulnerable columns 3and4  
![alt text](https://thelastvvv.github.io/images/posts/5/sql_5.png "sql5")

- Defend: 

Top 3 method of preventing SQL injection attacks ""

- Prepared statement: “make sure that the parameters (i.e. inputs) passed into SQL statements are treated in a safe manner.” - Escaping Inputs: using the strings escaping   to avoid characters that could lead to a malicious SQL command. 
Example: 
```sh
$firstname = $mysqli -> real_escape_string($_POST['firstname']); 
$lastname = $mysqli -> real_escape_string($_POST['lastname']); 
$age = $mysqli -> real_escape_string($_POST['age']); 
```

 - Sanitizing Inputs: the developers need to create a strong validations checker for all forms that helps to reject inputs that look suspicious automatically 


### Cross site-scripting
Is a vulnerability that allow the threat actor attack to inject malicious script in the vulnerable website which can lead to client-side attack in other meaning the threat actor can attack another user withing the vulnerable website   
Attack: 
In this case we will have a look of persistent cross site scripting of a vulnerable WordPress plugin that can lead to administrator and user's session hijacking or phishing attack that can results of compromised the website. 
![alt text](https://thelastvvv.github.io/images/posts/5/xss_1.png "xss1")
The threat actor can inject a malicious JavaScript into the registration form 
![alt text](https://thelastvvv.github.io/images/posts/5/xss_2.png "xss2")
Which resulted in successful running the malicious JavaScript in admin panel of WordPress user. 
![alt text](https://thelastvvv.github.io/images/posts/5/xss_3.png "xss3")
Defend:  
- Escape Dynamic Content: replacing significant characters (JavaScript) with the HTML entity encoding  
- Implementing  web application/server  firewalls like ( i.e. Akamai Edge, Cloudflare) 
- As normal user daily updating your plugins and remove inactive ones  

### Security Misconfiguration
Attack : 
From webserver Linux point of view , SUID means set user id , some files in Linux have some specific permission different from  r-w-x  this permissions are set by the owner of file . but in same binaries and files could be owned by root but other users are allowed to run it as result  sometimes in misconfiguration and unrestricted on authentication of the users. 
![alt text](https://thelastvvv.github.io/images/posts/5/sec_1.png "sec1")
The threat actor can preform Privilege escalation from a normal user in system to root . 
![alt text](https://thelastvvv.github.io/images/posts/5/sec_2.png "sec2")
As we can see  this system can be exploited by  runing sudo superuser command in ENV binary that results an access to the file system, escalating or maintain privileged access. 
![alt text](https://thelastvvv.github.io/images/posts/5/sec_3.png "sec3")
Defend: 

- "Secure installation processes"
- "A task to review and update the configurations appropriate to all security."
- "An automated process to verify the effectiveness of the configurations"

## Software Security
Software Security is important to to protect and secure softwares from threats and risks
### Buffer Overflow
 Buffer overflow:  occurs when a program tries to store more data in a temporary storage area than it can hold 
Attack (stack demo): 
![alt text](https://thelastvvv.github.io/images/posts/5/buff_1.png "buffer")
in code above we can say user required to enter the name if the is match the name we stored it will create text file on the desktop (edited version of James Lyne)
![alt text](https://thelastvvv.github.io/images/posts/5/buff_2.png "buffer2")
The C code have a variable char name have 16 bits what we cand see the that we exceeded the number of bits it starts over flow the second variable int which resulted in execution command if (namecheck) then created text file in the desktop 
Defend: 
- Better coding practices and security software implementation. 
- Non-executable stack:  configured the stack to not have any executable code. 
- Static Analysis:  analysis the source code from dangerous library calls ,strings and functions.

## IP Security
IP: Internet Protocol address is a unique address assigned to a device on the local network or on the internet  
IP security: is security implantation which adds layers of encryption and authentication to the IP. 
Top IPsec benefits: 
- Secure routing 
- VPN over internet  
- Secure remote access 

IP sec pros and cons: 
Pros: 

- Supplies confidentiality, authenticity, and integrity 
- Anon identity of the network 
- Secure network than without any security layers 

Cons: 

- One problem can cause issues with full network 
- VPN gateways can be hacked 
- NAT and Firewall traversal are not easy to solve

## Email-Security
 Email security is particularly important because of the sensitive information that countians but also the wide range if usage of emails is part of our daily checkup routine that why we need to learn how to email security works and how we need to do to be safe. 
Most of emails gateways come with some specific security layers like: 
- Anti-virus Protection 
- Data Encryption 
- Spam filtering 

But all these measures are not enough we need to make sure we are doing a secure login, having strong password, not opening random and spam emails, or downloading the attachments. As for companies they need to create a program with new policies and rules that change Frequently change password, and avoid sharing sensitive information and use of company emails without a secure connections like VPN. 
## Conclusion
 At end the users of internet should learn and understand cyber security and also security expert should teach and contribute to the community and encourage the new comers and curious people because security is not about secure coding but also a life style, information security is wide range of fields and topic can be presented in different ways at end is to archive one goal a secure and safe cyberspace for everyone.
 
 
##### Reference:
https://www.w3schools.com/php/func_mysqli_real_escape_string.asp
https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
https://redtiger.labs.overthewire.org/
https://gtfobins.github.io/gtfobins/env/
https://www.geeksforgeeks.org/ip-security-ipsec/
https://www.cse.wustl.edu/~jain/cis788-97/ftp/ip_security/index.html
https://forum.huawei.com/enterprise/en/advantages-and-disadvantages-of-ipsec/thread/567725-867
https://nvd.nist.gov/vuln/detail/CVE-2020-15536
https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15536








