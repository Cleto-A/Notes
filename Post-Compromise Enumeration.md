# Post-Compromise Enumeration

## Power-view

[Powerview GitHub](https://github.com/PowerShellMafia/PowerSploit/blob/master/PowerSploit.psd1)

[Powerview cheatsheet](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993) 

This script is ran directly on a user machine or remotely from yours - this tool is for enumeration.

1. Once powerview is downloaded, open up CMD in the directory where powerview is in and run..

```powershell
powershell -ep bypass
```

 
![Untitled](https://user-images.githubusercontent.com/55252902/166306548-cc9819bc-636b-43cb-b884-dda4dd8e90bc.png)


Bypass execution policy so we can execute scripts.

1. Call powerview

![Untitled 1](https://user-images.githubusercontent.com/55252902/166306559-fa64ab6a-3e6f-47f6-8bb1-c822a6a9acd8.png)


1. Nothing will be shown after pressing enter, but powerview is loaded.
- Get-UserProperty  -Properties logoncount - If last logoncount is 0, potentially that account could be a honeypot
