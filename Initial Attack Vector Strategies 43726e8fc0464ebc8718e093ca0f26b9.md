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
    - Jenkins - Check for web logins for developer pages, enumerate further.
    - Etc
- Think outside the box

[LLMNR Poisoning | MITM](Initial%20Attack%20Vector%20Strategies%2043726e8fc0464ebc8718e093ca0f26b9/LLMNR%20Poisoning%20MITM%207d8678bdde8c4f2a856c4c3dfcc38c53.md)

[SMB Relay Attack](Initial%20Attack%20Vector%20Strategies%2043726e8fc0464ebc8718e093ca0f26b9/SMB%20Relay%20Attack%20b40788850b4c4f5e958f89463d1db0ad.md)

[IPv6 Attacks](Initial%20Attack%20Vector%20Strategies%2043726e8fc0464ebc8718e093ca0f26b9/IPv6%20Attacks%200b9330add69b4c9485f9176ec849bd0a.md)

[Bloodhound](Initial%20Attack%20Vector%20Strategies%2043726e8fc0464ebc8718e093ca0f26b9/Bloodhound%20f824389592304db99e91902d158d486c.md)