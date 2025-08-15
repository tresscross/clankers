This challenge provided you with a PCAP, investigative flow looked like:
- review pcap, notice not too many packets
- use statistics > analyze > http > requests
	- very clearly some suspicious commands and things being done
- hone in on those IP addresses, use filters in wireshark such as `http` and `ip.addr` to review packets
- download `avp.msi` malware via 