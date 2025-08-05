# Virtualization-System-based-on-Proxmox
## I. Overview

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

Finally, the hardware we will go with 2 processors and 8 GB which is recommended or there will be some warning. And don't forget about the nested virtualation. 

<img width="494" height="138" alt="image" src="https://github.com/user-attachments/assets/e1d2f12f-6ff2-4dad-879e-2e999ba64319" />


Ok about configure the vt-x, when I choose Vmware Workstation Pro which is great as there are many free key in the internet easy access. How ever there's a problem with the vt-x which is this option in Vmware that i couldn't turn them on, it keeps saying "Virtualized Intel VT-x/EPT is not supported on this platform".

<img width="492" height="117" alt="image" src="https://github.com/user-attachments/assets/f3b4fefb-88d5-4033-a129-70b8b9f1fd40" />

Ok i used this post to fix it [https://community.broadcom.com/vmware-cloud-foundation/discussion/vmware-workstation-17-pro-virtualized-intel-vt-xept-is-not-supported-on-this-platform](https://learn.microsoft.com/en-us/answers/questions/751566/vmware-workstation-does-not-support-nested-virtual) I've turn on vt-d and any thing relate to vt-x, that is the solution. Be carefull with what you've turn off this may make the internet features like vpn goes wrong (as i did). I reset the PC configuration to fix it which is a bad solution but i had destroy all of my driver config. I got some trouble in configure group policy in Window 11 Home Sigle Language which does not give a lot of control for example group policy and hyper V (at first i thought it wasn't there beacause my version is too new) so i decide to buy a key Window 11 Pro, and so it turns out that you cannot directly to Window 11 Pro but gotta use public key for not active version in Window 11 Pro. That's a lot of stuff to go though, just to turn on one option.   

Next about the setup when booting, i choose graphical for better UI, of course. After click to one option in the boot menu. Just fill your country then next fill the password and real email for notification. 

About the host name i just go to change them a little bit because there will be another 2 nodes for a cluster. 

<img width="1207" height="793" alt="image" src="https://github.com/user-attachments/assets/5baf1673-1fd2-4b19-ae15-ae48168eb62f" />

Check your info last time and then done, reboot~


b) How to create a cluster in Proxmox

c) How to use CEPH and OSD in Proxmox

d) ZFS configure in Proxmox

e) HAProxy and pfSense (Self-host a Server)

### 3. Use-case 2: Proxmox VE HA Manager

### 4. Use-case 3: Live/Online migration

### 5. Use-case 4: Proxmox VE Firewall

### 6. Use-case 5: Proxmox Backup and Restore 
