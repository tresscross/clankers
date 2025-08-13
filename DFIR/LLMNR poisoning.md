- Link-Local Multicast Name Resolution performs name resolution for hosts on the same local network.
- If a request to a DNS server fails (e.g., if a DNS server is not available), an LLMNR query is made across the local network to attempt to resolve that request.
The attack:
- attacker is listening for LLMNR requests
- when request is made across the local network, the attacker's device responds with its own IP address, redirecting the network traffic

Tooling used to do this:
	[Responder](https://www.kali.org/tools/responder/)