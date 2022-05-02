# IPv6 Attacks

Another form of relaying using IPv6. Most machines on a Windows network run on IPv4. IPv6 may be turned on and is not being utilized. most of the times no one is doing DNS for IPv6. An attacker machine can perform a mitm attack by spoofing IPv6 DNS.  IPv6 traffic will be redirected to the attacker machine. From here you can get authentication to a DC via LDAP or SMB. You can wait for someone to log-in to the network and use their credentials, this comes in the form of NTLM (LDAP relay).  

Mitm6 is a pentesting tool that exploits the default configuration of Windows to take over the default DNS server. It does this by replying to DHCPv6 messages, providing victims with a link-local IPv6 address and setting the attackers host as default DNS server. As DNS server, mitm6 will selectively reply to DNS queries of the attackers choosing and redirect the victims traffic to the attacker machine instead of the legitimate server. For a full explanation of the attack, see our blog about mitm6. Mitm6 is designed to work together with ntlmrelayx from impacket for WPAD spoofing and credential relaying.

## Lab configuration

Server manager > Mange > Add Roles and Features 

![Untitled](https://user-images.githubusercontent.com/55252902/166305257-c3be0eb4-2230-4173-8618-058ca2c7a343.png)

Setting up a certificate so we can run LDAP secure (ldaps).

## IPv6 DNS Takeover

```bash
mitm6 -d <domain-name>
```

![Untitled 1](https://user-images.githubusercontent.com/55252902/166305350-7f46bfb2-59fd-47b9-bbf9-854193f057c7.png)


```bash
ntlmrelayx.py -6 -t ldaps://<domain-controller-ip> -wh falsewpad.BLEACH.local -l lootme
```

- 6 - Stands for IPv6
- t - target
- wh - WPAD
- l - Stands for loot, dumping information

![Untitled 2](https://user-images.githubusercontent.com/55252902/166305364-f707645f-03f5-4ff7-965a-01aaeed19672.png)


> The **Web Proxy Auto-Discovery (WPAD) Protocol**
 is a method used by clients to locate the URL of a configuration file using [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol)
 and/or [DNS](https://en.wikipedia.org/wiki/Domain_Name_System).
> 

IPv6 sends out a reply asking “Whose got my DNS?” on a interval. To speed this up for lab purposes, I am going to restart a machine that is connected to the domain. 

![Untitled 3](https://user-images.githubusercontent.com/55252902/166305388-86d18ff6-71b5-48ec-9f62-149596eb770d.png)


Replies are coming back now, domain info dumped into lootdir.

![Untitled 4](https://user-images.githubusercontent.com/55252902/166305399-f9f6d300-19ca-4864-9e25-272c5ece3322.png)

![Untitled 5](https://user-images.githubusercontent.com/55252902/166305408-b2160a5c-a289-4f3d-ae30-fba609797b0a.png)

TONS OF INFORMATION!

![Untitled 6](https://user-images.githubusercontent.com/55252902/166305420-65528c1a-60b4-4a9f-bbf6-e15c2ce65299.png)

Logged into a machine as Administrator. 

![Untitled 7](https://user-images.githubusercontent.com/55252902/166305432-6affe2d7-8a09-4657-9957-6b374e59245e.png)

![Untitled 8](https://user-images.githubusercontent.com/55252902/166305444-40f9822c-f677-4539-ac67-8d0ffba1ea13.png)

![Untitled 9](https://user-images.githubusercontent.com/55252902/166305458-358c9240-f545-45cd-90c3-c2f676c38167.png)

![Untitled 10](https://user-images.githubusercontent.com/55252902/166305473-ad3d1e01-31a9-4721-b6ef-9e13d9cdbb87.png)


ACL (Access Control List) allows user through because of this ACL via this attack. 

New users were added by they are not displaying the username and password in the terminal.

## Disclaimer

In a real engagement/enviorment you can potentially receive 1000’s of request for IPv6 DNS queries and mitm6 will redirect those request to the domain controller via ntlmrelayx. This can cause a temporary DoS.

What you can do in an environment that is large and during a time period such as lunch is to target specific IPs and relay those to the domain controller.  For example, if you know a domain admin is at 192.168.5.15, you would target that IP specifically vs 1000 IPs.

There wouldn't be 200 DAs (unless something is really wrong),  a new account is created every time, so in theory, yes 200 accounts would be created if you did not stop the relays with a Ctrl + C.

## Mitigation Strategies

1. IPv6 poisoning abuses the fact that Windows queries for an IPv6 address even in IPv4-only environments. If you don’t use IPv6 internally, the safest way to prevent mitm6 is to **block DHCPv6 traffic and incoming router advertisements in Windows Firewall via Group Policy.** Disabling IPv6 entirely may have unwanted side effects. Setting the following pre-defined rules to Block instead of Allow prevents the attacker from working:
    1. (Inbound) Core Networking - Dynamic Host Configuration Protocol for IPv6(DHCPV6-In)
    2. (Inbound) Core Networking - Router Advertisement (ICMPv6-In)
    3. (Outbound) Core Networking - Dynamic Host Configuration Protocol for IPv6(DHCPV6-In)
2. If WPAD is not in use internally, disable it via Group Policy and by disabtling the WinHttpAutoProxySvc service.
3. Relaying to LDAP and LDAPS can only be mitigated by enabling both LDAP singing and LDAP channel binding.
4. Consider Administrative users to the Protected Users group or marking them as Account is sensitive and cannot be delegated, which will prevent any impersonation of that user via delegation.

## Sources
[Github - Mitm6](https://github.com/dirkjanm/mitm6)

[Kerberoes Delagation](https://dirkjanm.io/worst-of-both-worlds-ntlm-relaying-and-kerberos-delegation/)

[Mitm6 IPv6](https://blog.fox-it.com/2018/01/11/mitm6-compromising-ipv4-networks-via-ipv6/)

