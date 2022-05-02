# Kerberoasting

# SPN - Service Principal Names

[Service Accounts (SPN)](Kerberoasting%20f96b27d162554eae8993a450b617671e/Service%20Accounts%20(SPN)%2066fb82ecfb79480aa852482e3147d6f5.md)

SPNs are used by Kerberos authentication to **associate service instances with a service logon account.** SPN acts as a pointer to that domain account that is running a service. When something wants to request access to that service, it doesn’t need to know the actual domain account that is running that service. **That something just wants access to service X on machine Y.**

### Example:  MSSQLsvc/sql1@domain.local

If something were to request access to this example service...

- They would request access to - MSSQLsvc
- Running on this machine - sql1
- Apart of this domain - @domain.local
- Something requesting access to this service doesn’t need to know the name of this account, it just wants access to a particular service.

![Untitled](https://user-images.githubusercontent.com/55252902/166307364-0a2860ad-9969-487b-85f9-16b6f62c6275.png)


## Requirements to perform Kerberoasting

- Requires access to a domain - Running commands as a user to the domain - or - Running remotely from a different machine that is connected to a domain (Doesn’t need to be privileged, any user account).

## Focus

- We can KRB_TGS_REQ (Request Ticket Granting Service) any account that has a **SPN tied to it** from a **valid domain account**.
- In return we get KRB_TGS_REP (Ticker Granting Reply) - Encrypted with NTLM hash of the actual domain that the request service is running as.
- Take the TGS_REP and extract the NTLM hash, take offline and crack it.
- Leading to lateral movement and privilege escalation.
- Service accounts can be misconfigured, for example service accounts that are running as domain admins. More than likely a service account will have a SPN tied to them. Anybody in the domain can essentially request hash of that domain account.

## Exploitation

Impacket has a tool called GetUserSPNs, you need credentials for a domain account, unless you’re running it directly on the machine that you want to kerberoast from. This is done remotely.

```bash
GetUsersSPN -dc-ip= <domain-ip> <domainname.local/domainusername>
```

You will see accounts that do have SPN tied to them and what group/groups they are member of.

```bash
GetUsersSPN -dc-ip= <domain-ip> <domainname.local/domainusername> -request
```

This command will perform that kerberos authentication process and attempt to get a hash back.

This hash can now be taken offline and potentially cracked.

![Untitled 1](https://user-images.githubusercontent.com/55252902/166307376-1bee41f2-afd5-46f1-a9ef-0b64f73bf5cf.png)

## Mitigations

- Long and complex passwords for all accounts but especially for accounts that have SPNs tied to them. Rotate them twice.
- Rotated/change passwords
- Service accounts have the least amount of privilege. Do not put these accounts into groups they don’t need to be (Domain Admin).

## Sources
