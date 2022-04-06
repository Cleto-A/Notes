# Cybersecurity Home Lab
I am a highly hands-on person, this is how I learn best and what I enjoy. For my big project I am setting up a small enterprise network in my homelab to broaden my understanding and grasp of things firsthand. The goal of this exercise is to walk through the process of installing, configuring, and optimizing systems on a modest scale to mimic a corporate network. I will be going over different attack methods on my own enterprise network along with defenses and counter measures against them. I will do what is possible with my current computer resources. I will be doing this all through VMware workstation 16 player.


## System Specs

CPU - AMD Ryzen 5 2600

Ram - 32 GB 3000 MHz

GPU - RTX 2080


# Homelab Topology
Firstly, all of this could be subject to change but for now this is the blueprint that I will be following. I've also for quite a while now have had my Active Directory server and both windows machines set up already. I followed [Heath Adams tutorial](https://www.youtube.com/watch?v=xftEuVQ7kY0) on how to set that up. 

![networkdiagram](https://user-images.githubusercontent.com/55252902/162085140-0b8bc10a-8bb1-4bd7-b735-7bb6c08e248d.png)


# Firewall - pfSense
Downloading the latest version of pfSense, I followed this [Guide](https://www.vgemba.net/vmware/pfSense-VMware-Workstation/) in setting pfSense up as a VM. By doing this, I can isolate my lab enviorment behind the firewall so that whatever I do in my lab enviorment does not affect my home network. I followed best current practices with initial configurations while documentating my changes. I will be monitoring and making adjustments as I go.


Current timeline as of 4/6/22
For now this is what I have set up. I will be continuing my studies and further expanding on my homelab. Changes or additions I make, I will be documenting and uploading here.




