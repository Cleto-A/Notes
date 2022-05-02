# GPP- Credentials | Lateral Movement and Privilege Escalation

[PowerSploit - GitHub](https://github.com/PowerShellMafia/PowerSploit)

## Hunting for passwords by GPP (Group Policy Preferences).

**Group Policy Preferences / GPP can be used to set passwords for local accounts in an active directory environment, among other things**. **These passwords are stored in a way that any user or machine can retrieve them and decrypt them, resulting in privilege escalation or lateral movement for an attacker.** This method is extremely useful for pentesting active directory environments and real world pentesting.

A set of client side extensions that allows admins to configure more options with group policies.

- Setting local users passwords
- Mapping shared drives
- Adding local users to groups

All of these actions require a password to be entered and stored into a GPP object.

Due to how GPP objects are distributed to clients, they are stored in the SYSVOL share of share of domain controllers and all authenticated users are given access. 

Any authenticated user account is able to **retrieve and read** GPP objects.

These passwords aren’t stored in plaintext, they are encrypted with an AES-Encryption algorithm. Back in 2012, Microsoft disclosed the AES key.

[AES Key - Microsoft](https://adsecurity.org/?p=2362)

Microsoft doesn’t allow you to use GPP to set passwords anymore. 

Can’t be done in modern domain controllers but can be done in Windows 2012 Server.
