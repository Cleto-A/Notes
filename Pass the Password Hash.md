# Pass the Password / Hash

## Pass the Password / Pass the Hash

If you’ve cracked a password or can dump the SAM hashes, you can leverage both for lateral movement in network.

Be careful password spraying on domain accounts. If there are a lot of machines and you pass a username/password around, those credentials are going to be sprayed many times and there is going to be a lot of failed login attempts. That user is going to get locked out.

**Local accounts don’t have the same lockout policies as domain accounts do. It may be better to password spray on local accounts than domain accounts.**

[CrackMapExec GitHub](https://github.com/byt3bl33d3r/CrackMapExec)

```bash
crackmapexec <ip/CIDR> -u <user> -d <domain> -p <password>
```

```bash
crackmapexec <ip/CIDR> -u <user> -d <domain> -h <hash> -local
```

crackmapxec takes the inputed password or hash and throws it around the specified subnet.

- You can also pass credentials around locally using -local flag.
- Sometimes Administrator reuse the same account and password to set up machines.
- Might need to specify smb before any other flag.

Use psexec or similar tools to authenticate as other users.

```bash
psexec.py <domainname/user>:<password>@<other-user-ip> 
```

### Can also use Metasploit windows/smb/psexec and meterpreter
