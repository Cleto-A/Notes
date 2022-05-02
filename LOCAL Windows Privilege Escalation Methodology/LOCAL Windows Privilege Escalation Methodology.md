# LOCAL Windows Privilege Escalation Methodology

![Untitled](https://user-images.githubusercontent.com/55252902/166310292-92f18b4c-40f1-41fa-b1d2-896f1c713160.png)


## Credential Access

![Untitled 1](https://user-images.githubusercontent.com/55252902/166310305-7dac0b65-9e91-4b1a-b603-f522c15c521b.png)


- Reused Passwords - Already have credentials? Check to see if the administrator is lazy and is reusing passwords.
- Credentials from Configuration Files - Any services that are running, check the configuration files that can be read and see if there are any credentials there.
- Credentials from Local Database - Can you log into the database? Perhaps you can extract credentials (hashed or plaintext).
- Credentials from cmdkey - Credentials can be stored in cmdkey.
- Credentials from Registry - Commands that query places in the registry for plaintext credentials.
- Credentials from Unattended(XML) or Sysprep files - These files are used for automatic installs of windows. Sometimes you can find credentials for autolog on or any other type of credentials.
- Credentials from Log Files - Authentication logs has users names and passwords.
- User groups - What groups are the user apart of? Maybe they share resources with another user or administrator.

## Exploit

![Untitled 2](https://user-images.githubusercontent.com/55252902/166310326-7dd1e02b-0691-4919-9d99-146e0e789da5.png)


- Services Running on [Localhost](http://Localhost) - Look at services that are running and the versions of them.
- Kernel Version - Check for kernel exploits.
- Software version and Service Version - What software and version are being run. Software could potentially be run as a high privilege account. Perhaps some RCE or local privilege escalation.

## Misconfigurations

![Untitled 3](https://user-images.githubusercontent.com/55252902/166310351-e18a7f59-45f8-4560-8828-e0d5b0b96ca8.png)


## Sources

[Conda OSCP Privilege Escalation Guide](https://c0nd4.medium.com/oscp-privilege-escalation-guide-4b3623f57d71)

[fuzzysecurity Windows Privilege Escalation](https://www.fuzzysecurity.com/tutorials/16.html)

[PayLoadsAllTheThing Windows - GitHuB](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)

[PowerSploit - GitHub](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1)
