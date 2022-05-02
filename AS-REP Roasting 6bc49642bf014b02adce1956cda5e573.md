# AS-REP Roasting

[https://www.qomplx.com/qomplx-knowledge-what-is-as-rep-roasting/](https://www.qomplx.com/qomplx-knowledge-what-is-as-rep-roasting/)

![Untitled](AS-REP%20Roasting%206bc49642bf014b02adce1956cda5e573/Untitled.png)

- Client sends a request for a TGT (Ticket Granting Ticket) to the KDC (Key Distribution Center).
- In that request, **the client is going to be sending an encrypted timestamp along with the request**. That timestamp is encrypted with the users password. KDC receives that request and decrypts it with the users password. **This verifies the person initiating the AS_REP request is the actual user and verifies that the client is not doing a replay attack.**
- Time is important in the kerberoast authenticating protocol. ERROR: CLOCK_SKEW if your system clock is too far off from the KDC.
- Once KDC verifies the KRB_AS_REQ, it is going to send back a KRB_AS_REP (Reply). This reply is going to contain a TGT and some data encrypted with the client’s password.
- Bruteforce (offline) the section with the client’s password.

## Requirements

![Untitled](AS-REP%20Roasting%206bc49642bf014b02adce1956cda5e573/Untitled%201.png)

- Kerberos-Pre-Auth needs to be disabled / Do not require Kerberos preauthentication.
- We don’t need to send an encrypted timestamp, the KDC won’t have to verify with a timestamp. We don’t need to know the users password.
- If a user account has Kerberos-Pre-Auth disabled, they can send a plain KRB_AS_REQ and receive back a TGT encrypted with the client’s password.

## Exploitation

Tool from Impacket called GetNPUsers. You don’t need a users password, so it is important to specify -no-pass in the script. You do need a list of users with UF_DONT_REQUIRE_PREAUTH.

This tool is for user accounts that don’t have Kerberos pre-auth enabled 

```bash
GetNPUsers <domainname.local/filecontainingusernames.txt -dc-ip= <domain-ip>
```

- Once executed it will send that KRB_AS_REQ.

![Untitled](AS-REP%20Roasting%206bc49642bf014b02adce1956cda5e573/Untitled%202.png)

Bruteforce the hash offline with hashcat or john. 

Once you have the password you can RDP, use evil-winRM, etc... into the machine

## Detection and Mitigation of AS-Rep Roasting attacks

- Enforce robust password policies for service accounts - Mandate long and complicated passwords **< 25 characters**. Make these passwords changed frequently, Ex: 30-day intervals, narrows the window of time attackers have to crack long hashes.
- Kerberos Monitoring - Technology such as Qomplx’s monitors for telltale signs of AS-REP roasting attacks, such as AS-REQ and AS-REP events in conjunction with unusual combinations of events like 4768 (TGT requested) followed by an invalid password credential (4625).
- Deploy Honey Accounts  - **As with Kerberoasting, detection of AS-REP roasting attacks requires logging and monitoring of activity.** One way to make sure such activity gets noticed is with the use of so-called “honey accounts,” which work in a similar fashion to network honeypots: enticing advanced attackers doing reconnaissance through Active Directory with believable sounding service names. **Once compromised, however, these accounts do nothing but trigger an alert if they are used to login or generate a service ticket request.**