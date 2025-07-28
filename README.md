# EDR Home Lab: Attack and Defense

## Projects:
This lab is dedicated to simulating a real cyber attack and endpoint detection and response. Utilizing Eric Capuano's guide online, I will be using virtual machines to simulate the threat & victim machines. The attack machine will utilize 'Sliver' as a C2 framework to attack a Windows endpoint machine, which will be running 'LimaCharlie' as an EDR solution.

Eric Capuano's Guide: https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-20 

#


## Setup
The first step to the lab is setting up both machines. The attack machine will run on Ubuntu Server, and the endpoint will be running Windows 11. I am going to be installing Sliver on the Ubuntu machine as my primary attack tool, and setting up LimaCharlie on the Windows machine as an EDR solution. LimaCharlie will have a sensor linked to the windows machine, and will be importing sysmon logs.
#

Windows 11 Machine - Installation of Lima Charlie - 
<img width="1189" height="660" alt="Installation for lima Charlie on Windows VM" src="https://github.com/user-attachments/assets/1eca91d5-b991-4e63-a625-d3ed50081642" />
<img width="1050" height="1117" alt="Setting up Lima Charlie Installation" src="https://github.com/user-attachments/assets/19dc379c-bb83-4359-9e73-8831cd8496b0" />
# 
# The Attacks, and the Defense
The first step is to generate our payload on Sliver, and implant the malware into the Windows host machine. Then we can create a command and control session after the malware is executed on the endpoint. 
# 

<img width="1007" height="910" alt="Linux silver status" src="https://github.com/user-attachments/assets/48fef2c4-af6a-48db-92bd-088ca45e9f5c" />
<img width="1039" height="472" alt="Picture 2" src="https://github.com/user-attachments/assets/52220eb8-bcfe-40cd-841b-d6e899ffc128" />
<img width="1913" height="390" alt="Picture 3" src="https://github.com/user-attachments/assets/30073cb9-0911-44a3-800e-44b990e8ed58" />
<img width="1724" height="233" alt="Picture 4" src="https://github.com/user-attachments/assets/79a9fcf4-b17c-4063-a1a1-f1fc6f9d5b55" />

#

Now that we have a live session between the two machines, the attack machine can begin peeking around, checking privileges, getting host information, and checking what type of security the host has.

<img width="1212" height="902" alt="Picture 5" src="https://github.com/user-attachments/assets/2962d3f5-ab4b-443b-86d0-e24e9d31e7ec" />
<img width="1228" height="901" alt="Picture 6" src="https://github.com/user-attachments/assets/208bf56b-3a09-4f33-85fe-d6cb04a83c5e" />
<img width="890" height="901" alt="Picture 7" src="https://github.com/user-attachments/assets/c8fd5c9c-fb40-4f2b-a819-e035b0ade727" />
<img width="875" height="866" alt="Picture 8" src="https://github.com/user-attachments/assets/bf367188-7a17-4804-962c-d694899f19b0" />

#

On the host machine we can look inside our LimaCharlie SIEM and see telemetry from the attacker. We can identify the payload thats running and see the IP its connected to.

<img width="1913" height="900" alt="Picture 9" src="https://github.com/user-attachments/assets/52bad8b9-7388-4234-a30b-2bbf32637188" />
<img width="1915" height="904" alt="Picture 10" src="https://github.com/user-attachments/assets/ed1f4c51-d46c-41d1-b8e8-bef440e15dd7" />

#

We can also use LimaCharlie to scan the hash of the payload through VirusTotal; however, it will be clean since we just created the payload ourselves.

<img width="1384" height="676" alt="Picture 11" src="https://github.com/user-attachments/assets/1534a22c-fa54-4e72-9de1-9a7a1ad50d74" />
<img width="1803" height="686" alt="Picture 12" src="https://github.com/user-attachments/assets/285585bc-9044-4683-9926-69c2f27ff622" />


#

Now on the attack machine we can simulate an attack to steal credentials by dumping the LSASS memory. In LimaCharlie we can check the sensors, observe the telemetry, and write rules to detect the sensitive process.
<img width="1654" height="188" alt="Picture 13" src="https://github.com/user-attachments/assets/0535cd76-eeef-45f6-a6eb-7bfcf26ada50" />
<img width="1916" height="1026" alt="Picture 14" src="https://github.com/user-attachments/assets/4f951a5f-aa0a-4688-90e3-4b5a1542f707" />
<img width="1652" height="785" alt="Picture 15" src="https://github.com/user-attachments/assets/39262cd6-8600-41d1-b11e-dd8be7d7c760" />


#

Now instead of simply detection, we can practice using LimaCharlie to write a rule that will detect and block the attacks coming from the Sliver server. On the Ubuntu machine we can simulate parts of a ransomware attack, by attempting to delete the volume shadow copies. In LimaCharlie we can view the telemetry and then write a rule that will block the attack entirely. After we create the rule in our SIEM, the Ubuntu machine will have no luck trying the same attack again.



<img width="800" height="374" alt="Picture 16" src="https://github.com/user-attachments/assets/c547cf58-b3fc-4264-a671-baedb20c4753" />
<img width="1646" height="746" alt="Picture 17" src="https://github.com/user-attachments/assets/5d252b7a-2c04-4a21-94b2-d19d1306de36" />
<img width="1916" height="904" alt="Picture 18" src="https://github.com/user-attachments/assets/75b3f21f-7ecd-47dd-bd52-1b47c4034a6e" />
<img width="768" height="225" alt="Picture 19" src="https://github.com/user-attachments/assets/e9109ea5-63c9-4d6d-a61f-6a3fd125a586" />
<img width="1656" height="240" alt="Picture 20" src="https://github.com/user-attachments/assets/c7c01e8f-4b04-4905-9ed7-e007fc5765c0" />





