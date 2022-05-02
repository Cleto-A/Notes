# LOCAL Windows Privilege Escalation Methodology

![Untitled](LOCAL%20Windows%20Privilege%20Escalation%20Methodology%2060becff2e9374886a77fca535141b80d/Untitled.png)

## Credential Access

![Untitled](LOCAL%20Windows%20Privilege%20Escalation%20Methodology%2060becff2e9374886a77fca535141b80d/Untitled%201.png)

- Reused Passwords - Already have credentials? Check to see if the administrator is lazy and is reusing passwords.
- Credentials from Configuration Files - Any services that are running, check the configuration files that can be read and see if there are any credentials there.
- Credentials from Local Database - Can you log into the database? Perhaps you can extract credentials (hashed or plaintext).
- Credentials from cmdkey - Credentials can be stored in cmdkey.
- Credentials from Registry - Commands that query places in the registry for plaintext credentials.
- Credentials from Unattended(XML) or Sysprep files - These files are used for automatic installs of windows. Sometimes you can find credentials for autolog on or any other type of credentials.
- Credentials from Log Files - Authentication logs has users names and passwords.
- User groups - What groups are the user apart of? Maybe they share resources with another user or administrator.

## Exploit

![Untitled](LOCAL%20Windows%20Privilege%20Escalation%20Methodology%2060becff2e9374886a77fca535141b80d/Untitled%202.png)

- Services Running on [Localhost](http://Localhost) - Look at services that are running and the versions of them.
- Kernel Version - Check for kernel exploits.
- Software version and Service Version - What software and version are being run. Software could potentially be run as a high privilege account. Perhaps some RCE or local privilege escalation.

## Misconfigurations

![Untitled](LOCAL%20Windows%20Privilege%20Escalation%20Methodology%2060becff2e9374886a77fca535141b80d/Untitled%203.png)

## Sources

[https://c0nd4.medium.com/oscp-privilege-escalation-guide-4b3623f57d71](https://c0nd4.medium.com/oscp-privilege-escalation-guide-4b3623f57d71)

[https://www.fuzzysecurity.com/tutorials/16.html](https://www.fuzzysecurity.com/tutorials/16.html)

[https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology and Resources/Windows - Privilege Escalation.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)

[https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)