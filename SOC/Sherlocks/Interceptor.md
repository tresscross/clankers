This challenge provided you with a PCAP, investigative flow looked like:
- review pcap, notice not too many packets
- use statistics > analyze > http > requests
	- very clearly some suspicious commands and things being done
- hone in on those IP addresses, use filters in wireshark such as `http` and `ip.addr` to review packets
- download `.msi` malware via file > export objects > http
	- saved and uploaded to VT for SSDeep hash
	- VT also answered malware family, creation time, domain relations, ip relations, dll inside
- to find hostname i looked in packets infected host sent to api gateway, hostname is in json payload along with owner and OS version
- to decrypt, you need to look in the HTTP stream focusing on communication between infected host and stage 2 c2 domain