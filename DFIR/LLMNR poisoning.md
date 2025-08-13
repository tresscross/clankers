- Link-Local Multicast Name Resolution performs name resolution for hosts on the same local network.
- If a request to a DNS server fails (e.g., if a DNS server is not available), an LLMNR query is made across the local network to attempt to resolve that request.
The attack:
- attacker is listening for LLMNR requests
- when request is made across the local network, the attacker's device responds with its own IP address, redirecting the network traffic

Tooling used to do this:
	[Responder](https://www.kali.org/tools/responder/)

## Detection
- LLMNR runs on UDP port 5355 by default
- can look for protocol LLMNR in wireshark
- look for unusual responding hosts, can do fequency analysis for hosts that usually handle requests vs those who rarely do
- in a lot of environments LLMNR comes into play during typo'd requests, look at requests to see if pattern matches
- typically the DC should respond, if you can exclude DCs from query that is helpful

### Triage
- you can look for the rogue device hostname looking for initial `dhcp` grants, should include hostname in packetx
- after determining possible LLMNR poisoning, look at `smb2` packets for NTLM negotiation, looking for user's hashes being stolen
	- here you will want to enable hostnames in wireshark
	- view > name resolution > resolve network addresses
	- ![[Pasted image 20250813122820.png]]
- to stitch together what credentials w