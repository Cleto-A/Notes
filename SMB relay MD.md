# SMB Relay Attack

## What is SMB Relay

Instead of cracking hashes gathered with Responder, we can instead relay those hashes to specific machines and potentially gain access.

Packet level protocol | Packets get signed so SMB signing has to be disabled | If SMB signing is off, authenticity is never check.

[https://www.cloudflare.com/learning/network-layer/what-is-a-packet/](What is a packet)

SMB Port 445

[https://infosecwriteups.com/abusing-ntlm-relay-and-pass-the-hash-for-admin-d24d0f12bea0](Pass the hash)

[https://blog.fox-it.com/2017/05/09/relaying-credentials-everywhere-with-ntlmrelayx/](ntlmrelayx)

## Requirements

- SMB signing must be disabled on the target.
- Relayed user credentials **must be local ADMIN** on machine | Has to be two or more separate machines with SMB signing disabled.
- Make sure network discovery is enabled on both windows machines.

## SMB Relay

1. I am going to use Responder to listen, not respond, another tool will be used for this | Need to edit Responder’s config file.
   
   ![Untitled](https://user-images.githubusercontent.com/55252902/154788581-b6d7d42d-5241-47a5-8027-f81a7e94d0e7.png)

2. Run responder 
   
  ![Untitled 1](https://user-images.githubusercontent.com/55252902/154788587-a61a4525-b3f7-46e1-b418-d60ec8e1a2c6.png)
  

3. Tool that I will be using is ntlmrelayx from impacket. Identify a target and where I will relay to.

4. Dump out SAM file (hashes) | Usernames and hashes for local users on a computer | Offline and crack or pass hashes around to gain access to other machines. 

Make sure network discovery and file sharing enabled on both workstations

![Untitled 2](https://user-images.githubusercontent.com/55252902/154788589-08ecdc87-4799-4542-a917-3de336c9c353.png)


## How to check if SMB signing is on/off

There is a NMAP script I can use to check for this | This script will sweep the entire subnet that we are on. 

![Untitled 3](https://user-images.githubusercontent.com/55252902/154788591-e3ff3325-8e36-4964-889e-5816750d6fea.png)


IP - 192.168.11.179 is the domain controller and SMB signing is enabled and will not be able to relay to this machine.

IP - 192.168.11.183 is a workstation that has SMB signing off.

IP - 192.168.11.133 is another workstation that has SMB singing off | Not in the screenshot. 

Create a text document with the IPs of the vulnerable targets.

gedit targets.txt in the text document just add 192.168.11.183 for this attack demonstration. 

![Untitled 4](https://user-images.githubusercontent.com/55252902/154788598-97593f96-8064-467b-afd3-f9737eb594c7.png)


In Responder.conf make sure SMB = Off and HTTP = Off

![Untitled 5](https://user-images.githubusercontent.com/55252902/154788601-e524f114-c1b2-4f08-a568-cd2cd4177275.png)

Run responder like before

![Untitled 6](https://user-images.githubusercontent.com/55252902/154788603-51355933-5056-4f2d-848d-6132323f29a0.png)

Run ntlmrelayx

![Untitled 7](https://user-images.githubusercontent.com/55252902/154788605-ec908cc4-097c-4c57-bbb2-382e1f0d6318.png)

- -tf stands for targetfile which is our targets.txt which has the IP of one of our host
- Two of my host are running and my attacker machine
- The target machine I will point at my attacker machine

![Untitled 8](https://user-images.githubusercontent.com/55252902/154788610-46be3b2d-5f7d-484d-997a-2a0903a2fa62.png)

![Untitled 9](https://user-images.githubusercontent.com/55252902/154788613-9bee6057-fd6f-4174-86ab-01d683facec1.png)

This took forever to setup and configure. First I had to deal with installing the latest version of impacket because I was having issues with python and Kali. Then once I got that resolved I was having issues with performing the SMB relay attack. It kept failing or nothing would go through. SMB signing was disabled so that wasn’t the issue. Come to find out I was having DNS issues on AD DS (event issue 4013) I had to restart DNS. That DNS issue was in tandem with one of my machines  not connected to the domain for some reason? I just removed it from the domain and rejoined it, that solved it. This surely was a learning experience.

Now that the I got the hash lets relay them next.
