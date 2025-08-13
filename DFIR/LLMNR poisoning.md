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
- to stitch together what credentials were leaked 
	- User::Domain:ServerChallenge:NTProofStr:NTLMv2Response(without first 16 bytes)


john.deacon::NBFY:601019d191f054f1:c0cc803a6d9fb5a9082253a04dbd4cd4:082253a04dbd4cd4010100000000000080e4d59406c6da01cc3dcfc0de9b5f2600000000020008004e0042004600590001001e00570049004e002d00360036004100530035004c003100470052005700540004003400570049004e002d00360036004100530035004c00310047005200570054002e004e004200460059002e004c004f00430041004c00030014004e004200460059002e004c004f00430041004c00050014004e004200460059002e004c004f00430041004c000700080080e4d59406c6da0106000400020000000800300030000000000000000000000000200000eb2ecbc5200a40b89ad5831abf821f4f20a2c7f352283a35600377e1f294f1c90a001000000000000000000000000000000000000900140063006900660073002f00440043004300300031000000000000000000