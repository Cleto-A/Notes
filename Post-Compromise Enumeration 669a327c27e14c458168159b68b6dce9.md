# Post-Compromise Enumeration

## Power-view

[https://github.com/PowerShellMafia/PowerSploit/blob/master/PowerSploit.psd1](https://github.com/PowerShellMafia/PowerSploit/blob/master/PowerSploit.psd1)

[https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)  - Powerview cheatsheet

This script is ran directly on a user machine or remotely from yours - this tool is for enumeration.

1. Once powerview is downloaded, open up CMD in the directory where powerview is in and run..

```powershell
powershell -ep bypass
```

 

![Untitled](Post-Compromise%20Enumeration%20669a327c27e14c458168159b68b6dce9/Untitled.png)

Bypass execution policy so we can execute scripts.

1. Call powerview

![Untitled](Post-Compromise%20Enumeration%20669a327c27e14c458168159b68b6dce9/Untitled%201.png)

1. Nothing will be shown after pressing enter, but powerview is loaded.
- Get-UserProperty  -Properties logoncount - If last logoncount is 0, potentially that account could be a honeypot