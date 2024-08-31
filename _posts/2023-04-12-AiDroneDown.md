# AiDroneDown
Drone Detection and Attack using roboflow and aircrack.ng with whitelist option


AiDroneDown version: 1.1 FREE 
check the project here:

https://github.com/TheLastVvV/AiDroneDown

# Installation 
python3 libriaries :

`pip install -r requirements.txt`

Network Interface configuration :


`chmod +x install.sh`
`sudo ./install.sh`

# Usage:
`python3 gui.py`

# QUICK LOOK

![alt text](gui1.png "Title")


![alt text](gui2.png "Title")


![alt text](white.png "Title")


![alt text](attacks.png "Title")


# Troubleshooting:
 Problem scenario 1:
 If the program don’t open the detection frame 

solutions 1: check you connections to internet 

solution 2 : make sure you two network interface are up and 
runing

 solution 3 : check api is correct and end point availability 
 
solution 4 : check webcam is working and running on selection 

output ( in this code dev/vide0 ) change it to 1 ,2 , -1 dependswebcam output
 
 problem scenario 2 :
 
 if the attacks don’t work
 
 solution 1 : make sure that network adapter support packet injections and monitoring mode
 
 solution 2 : check network adapter is on monitor mode and 
 
install.sh run without errors

 solution 3 : check general setting if you put the correct information
 
 solution 4 : the attacks are only for wifi-based drones
 
 problem scenario 3 :
 cracking password don’t work
 
 solution 1: make sure you have text file of wordlist in same directory or selected directory path in general settings
 
 solution 2 : could be issue with format of wordlist
 
 solution 3 : no matching of of password in wordlist choose long and strong wordlist
 


# Frequently Asked Questions (FAQs)
 can you detect drone from upward direction ?
 
 Drone can be detected based on camera used and which direction 
and angle is directed 

do the detection detect other flying object ?

 Our detection detect drones only with our tested dataset, the 
accuracy and detection are depended on dataset selected 

what is the range of detection ?

 The range of detection depends of quality , resolution and field
 of view of the camera used during our testing we used 720p webcam that have range of 
detection can range approx 20 meters to 30 meters

 what type of attacks are used ?
 
 De-Authentication attack , Hanshake capture attack , bruteforce 
attack , Network hijacking attack .

 Can these attacks effect other networks ?
 
 These attacks can effect other networks in the nature of threat 
actor can change WiFi drone network ssid which will be hard to 
detect based or keyword network detection of ssids in this case 
we create whitelist so user can protect their network during 
attacks ,In other way once detection happen all network that are
 in permitter and are not protected will be attacked .



 # Warning: This program is for educational purposes only. The creators are not responsible for any misuse.

 
@Thelastvvv

aka Fahad A.A
