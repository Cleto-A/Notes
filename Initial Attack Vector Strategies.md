# Initial Attack Vector Strategies

## Strategies

- Begin with mitm6 or Responder - do an assessment for LLMNR and IPv6 on the network. Running both, especially Responder first to assess traffic and how the network is responding to you. Is the network giving you hashes? Are those hashes easy to crack? Is LLMNR disabled? Are they preventing against common attacks?
    - Responder runs multi-cast name resolution - is **a protocol based on the
    Domain Name System (DNS) packet format that allows both IPv4 and IPv6 
    hosts to perform name resolution for hosts on the same local link**
    - If noise is not a factor, run bloodhound - graphs AD relationships
- You want traffic to be generated so begin some scans (Nessus & Nmap). A good time to begin this is when people start coming into work, around 8am. Another good time is after lunch, when people are returning to their computers.
- If scans are taking too long, look (sweep) for websites that are within scope (module metasploit: http_version). This is less likely to be picked up because traffic is being made on 80/443, which is very common traffic vs port scanning devices on a network that can be picked up by a SIEM.
- Look for default credentials on web logins
    - Printers - Scan to computer feature - Sometimes a Admin will make a user who can scan from a printer to a computer via SMB a Domain Admin. Either that user is a SMB user or they’re using an individual account.
    - CD/CD (Dev) - Check for web logins for developer pages, enumerate further.
    - Etc
- Think outside the box

## Sources
[AD - Attack/Defense - GitHub](https://github.com/infosecn1nja/AD-Attack-Defense#discovery)

[Hacktrickz AD Methodology](https://book.hacktricks.xyz/windows-hardening/active-directory-methodology)
