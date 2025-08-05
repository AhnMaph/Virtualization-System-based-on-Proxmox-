# Virtualization-System-based-on-Proxmox
## I. Overview
Good tips: take snapshot everything or you gonna start over many times!!
This is a brief instruction on how building Virtualization System based on Proxmox. **Home Lab edition**. 
## II. Milestones
### 1. Use-case 1: Integrate CEPH with Proxmox and then mount LUN

a) How to create a Proxmox nested virtualiztion? 

We need to get Proxmox iso download here https://www.proxmox.com/en/
And get your self a virtual environment i go with vmware

<img width="756" height="573" alt="image" src="https://github.com/user-attachments/assets/0a538646-9fe9-40c4-9d8a-75f1e89f8fc1" />

Then create a new virtual machine:


Choose the iso file that you downloaded.

<img width="498" height="525" alt="image" src="https://github.com/user-attachments/assets/4c5e9b5b-ebcf-4635-a9ee-a7d92930b4f7" />

I choose debian 12x 64-bit OS as it is said proxmox is more easy to use in debian(?).  
<img width="495" height="518" alt="image" src="https://github.com/user-attachments/assets/d0e403bc-2433-4680-9358-1d8a84d5ffbf" />

<img width="498" height="520" alt="image" src="https://github.com/user-attachments/assets/b426058f-2071-4864-a8a2-c118c0d8cb68" />

<img width="496" height="531" alt="image" src="https://github.com/user-attachments/assets/0fc2ae2a-9fa2-4ac4-9d52-0a1c26247319" />
To connect with this vm thorough web ui we choose network adapter NAT. 

<img width="891" height="891" alt="image" src="https://github.com/user-attachments/assets/827a8438-f36a-4b4c-9d28-794217a4fb08" />


Finally, the hardware we will go with 2 processors and 8 GB which is recommended or there will be some warning. And don't forget about the nested virtualation. 

<img width="494" height="138" alt="image" src="https://github.com/user-attachments/assets/e1d2f12f-6ff2-4dad-879e-2e999ba64319" />


Ok about configure the vt-x, when I choose Vmware Workstation Pro which is great as there are many free key in the internet easy access. How ever there's a problem with the vt-x which is this option in Vmware that i couldn't turn them on, it keeps saying "Virtualized Intel VT-x/EPT is not supported on this platform".

<img width="492" height="117" alt="image" src="https://github.com/user-attachments/assets/f3b4fefb-88d5-4033-a129-70b8b9f1fd40" />

Ok i used this post to fix it [https://community.broadcom.com/vmware-cloud-foundation/discussion/vmware-workstation-17-pro-virtualized-intel-vt-xept-is-not-supported-on-this-platform](https://learn.microsoft.com/en-us/answers/questions/751566/vmware-workstation-does-not-support-nested-virtual) I've turn on vt-d and any thing relate to vt-x, that is the solution. Be carefull with what you've turn off this may make the internet features like vpn goes wrong (as i did). I reset the PC configuration to fix it which is a bad solution but i had destroy all of my driver config. I got some trouble in configure group policy in Window 11 Home Sigle Language which does not give a lot of control for example group policy and hyper V (at first i thought it wasn't there beacause my version is too new) so i decide to buy a key Window 11 Pro, and so it turns out that you cannot directly to Window 11 Pro but gotta use public key for not active version in Window 11 Pro. That's a lot of stuff to go though, just to turn on one option.   

Next about the setup when booting, i choose graphical for better UI, of course. After click to one option in the boot menu. Just fill your country then next fill the password and real email for notification. 

About the host name i just go to change them a little bit because there will be another 2 nodes for a cluster. 

<img width="1207" height="793" alt="image" src="https://github.com/user-attachments/assets/5baf1673-1fd2-4b19-ae15-ae48168eb62f" />

Check your info last time and then done, reboot~

<img width="1422" height="413" alt="image" src="https://github.com/user-attachments/assets/54e58da5-2e78-4a6e-addf-4c418a0c5797" />

<img width="1896" height="811" alt="image" src="https://github.com/user-attachments/assets/e3303e52-fec8-4c7f-8650-22b2d001fc5f" />

type password that you choose lately 

<img width="1917" height="884" alt="image" src="https://github.com/user-attachments/assets/c29723e5-3170-42fb-b1f1-076c503f0f42" />

<img width="1906" height="874" alt="image" src="https://github.com/user-attachments/assets/815b8fef-558a-486b-ac7f-52514b48e444" />

b) How to create a cluster in Proxmox
<img width="1906" height="817" alt="image" src="https://github.com/user-attachments/assets/1253b31d-bf51-4f8f-aa4e-a8068730f7b5" />

<img width="721" height="262" alt="image" src="https://github.com/user-attachments/assets/6d32f81e-6c8a-4d2d-b195-808094696b0b" />

<img width="915" height="543" alt="image" src="https://github.com/user-attachments/assets/08c0d2bc-5a53-45c8-8d1c-cba739175940" />

This is the info other node will have to paste in so that they can join the cluster:
<img width="1041" height="539" alt="image" src="https://github.com/user-attachments/assets/33d52fe3-1cd3-4b5f-9ce0-6a7950a0db4b" />

<img width="1212" height="628" alt="image" src="https://github.com/user-attachments/assets/14676684-7e0b-413d-b1a5-89a536002172" />

<img width="383" height="236" alt="image" src="https://github.com/user-attachments/assets/966053d1-5bd9-4061-9bee-7919f7185c4d" />

Refresh to get new info for new node:

<img width="393" height="177" alt="image" src="https://github.com/user-attachments/assets/e9c9eae2-64c5-45eb-8ee4-6e28c4965ce5" />

c) How to use CEPH and OSD in Proxmox
You only config CEPH once in master node (pve1):
<img width="1916" height="894" alt="image" src="https://github.com/user-attachments/assets/d8c36684-bb15-4924-b451-651e0861abac" />


Turn off your vm. Add another hardware for the OSD i go with 50GB as it just a homelab i am not sure which storage is suitable (saw many youtuber go beyond this):

<img width="320" height="513" alt="image" src="https://github.com/user-attachments/assets/aec9b3bc-7f4a-4efc-8eea-febb430b697c" />

<img width="883" height="897" alt="image" src="https://github.com/user-attachments/assets/ad0e9a63-2ada-4f90-a622-e83ab687d639" />

<img width="887" height="901" alt="image" src="https://github.com/user-attachments/assets/355be322-2d1e-4f7c-b839-4ca56334d149" />


Then start the vm, install CEPH, no-subscription: 
<img width="860" height="645" alt="image" src="https://github.com/user-attachments/assets/5fe51005-9182-4ea1-891a-0ccac1d73203" />


<img width="886" height="645" alt="image" src="https://github.com/user-attachments/assets/bfa993a1-8a51-4608-90a5-8d776592b544" />

<img width="892" height="663" alt="image" src="https://github.com/user-attachments/assets/824e1cde-40c1-4e6c-9b6c-7a12688143d1" />

Add the disk you just added, in this case i've already added so it show nothing.

<img width="1621" height="662" alt="image" src="https://github.com/user-attachments/assets/6cb21af1-37ec-4cd0-86cb-c6191452ce1e" />

Check the health status for any problem:

<img width="1912" height="644" alt="image" src="https://github.com/user-attachments/assets/4e028d3b-2ae6-43e7-8b2a-13f9551c9899" />



d) ZFS configure in Proxmox

e) HAProxy and pfSense (Self-host a Server)

### 3. Use-case 2: Proxmox VE HA Manager

### 4. Use-case 3: Live/Online migration

### 5. Use-case 4: Proxmox VE Firewall

### 6. Use-case 5: Proxmox Backup and Restore 
