# LLMNR Poisoning | MITM

## What is LLMNR | Responder

> [LLMNR/NBT-NS Poisoning on Windows Domain Environments | Predatech](https://predatech.co.uk/llmnr-nbt-ns-poisoning-windows-domain-environments/)

Used to identity host when DNS fails to do so.

When we respond to this service, it responds back to us with a **username** and a **password hash**

- Previously NBT-NS

- Key flaw is that the service utilize a user’s username and NTLMv2 hash when appropriately responded to.

Link-Local Multicast Name Resolution (LLMNR) and NetBIOS Name Service (NBT-NS) are two name resolution services that Windows machines use to identify host addresses on a network when DNS resolution fails. LLMNR and NetBIOS are enabled by default on modern Windows computers.

1. Check if the name resolves to the computer itself (localhost).

2. Check to see if the name is in the cache or manually specified in the system’s hosts file (C:\Windows\System32\drivers\etc\**hosts**

3. Send a lookup request to the configured DNS server.

4. Broadcast an LLMNR name query to all machines on the local network.

5. Broadcast an NBT-NS name query request to all machines on the local network.

6. The LLMNR and NBT-NS queries will be sent to all other hosts on the local network asking them to respond if they know the IP of the hostname being queried. Attackers can exploit this and will respond with their own IP address to direct subsequent network traffic for the requested resource to their machine.

![Untitled.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled.png)

## Step 1: Run Responder | python [Responder.py](http://Responder.py) -l tun0 -rdw

- -i stands for interface which should be eth0

Responder - responds to request | sit there and listen | Best time to run is first thing in the **morning** or **right after lunch**. | **You need a lot of traffic.** | MITM listening | Waiting

## Step 2: An event occurs

## Step 3: Hashes acquired

## Step 4: Hash cracking with hashcat | If passwords are weak | >14 Chars

```shell
hashcat -m 5600 hashes.txt rockyou.txt (or which ever wordlist)
```

# Demonstration

Run responder

```
responder -I eth0 -rdwv
```

![Untitled 1.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%201.png)

![Untitled 2.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%202.png)

Responder is running and listening

![Untitled 3.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%203.png)

![Untitled 4.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%204.png)

AD DS and workstation both running.

Point workstation to attack machineIP 

```shell
\\x.x.x.x
```

![Untitled 5.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%205.png)

Hashes pulled | Take offline and attempt to crack.

# Hashcat

Hashcat is a password recovery tool

Need to find which module to use for hashcat.

```shell
hashcat --help | grep NTLM
```

![Untitled 6.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%206.png)

I saved this hash in my main OS which has hashcat installed. I have a RTX 2080 so this crack should go pretty fast.

![Untitled 9.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%209.png)

Change drives and CD to where hashcat is.

```shell
hashcast-6.2.4>hashcat64.exe -m 5600 ntlmhash.txt rockyou.txt -O
```

![Untitled 10.png](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\Untitled%2010.png)

- The -O stands for optimize

![InkedUntitled 12_LI.jpg](C:\Users\jonne\Documents\PDF\pdfs\LLMNR%20Poisoning%20MITM%20710337978ef845858bd8ddf37d19c90d\InkedUntitled%2012_LI.jpg)

H**ashcat has tried every possible password combination in the attack you have provided**, and failed to crack 100% of all hashes given. In other words, hashcat
has finished doing everything you told it to do – **it has exhausted** its
search to crack the hashes.

Need another wordlist

The next attempt worked but I honestly had to add the passwords in myself. 
Rockyou.txt did not work and the wordlists from seclist either. I need 
to get better wordlists. It is a good thing this happened because it 
lets me know I need better wordlists.

# Defense to LLMNR Poisoning

The best defense is to **disable** LLMNR and NBT-NS

- To disable LLMNR select “Turn off Mutlicast Name Resolution” under Local Computer Policy > Computer Configuration > Administrative Templates > Network > DNS Client in the Group Policy Editor

- To disable NBT-NS, navigate to network connections > Network Adapter Properties > TCP/IPv4 Properties > Advanced tab > Wins tab and select “Disable NetBIOS over TCP/IP”.

Some companies must use or cannot disable LLMNR/NBT-NS, the best course of action is to

- Require Network Access Control (NAC)

- Require strong passwords (Ex: >14 Chars in length and limit common word usage). The more complex and long, the harder it is for an attacker to crack the hash. Make it as hard as possible. Prevent | Stall.

- Stress how easy it is to crack passwords.
