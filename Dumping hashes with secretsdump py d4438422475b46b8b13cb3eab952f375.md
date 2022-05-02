# Dumping hashes with secretsdump.py

Metasploit psexec dumping hashes is a bit on the noisy side and can be picked up by anti-virus or Windows Defender.

Psexec maybe...

## secretsdump.y

Part of the impacket tool kit

```bash
secretsdump.py <domainname/user:<password>@<target-ip>
```

Take these hashes and attempt to crack them offline with hashcat or john.

**You can pass around NTLM hashes but you CAN’T password NTLMV2 hashes**