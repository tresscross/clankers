ComputerName is in
`SYSTEM\ControlSet001\Control\ComputerName\ComputerName`

finding wifi SSID by looking in 
`\Windows\System32\winevt\Logs\Microsoft-Windows-WLAN-AutoConfig%4Operational.evtx`
- **Event ID 8001** (WLAN connected)

``` sh
chainsaw search -t 'Event.System.EventID: =8100' \Windows\System32\winevt\Logs\Microsoft-Windows-WLAN-AutoConfig%4Operational.evtx
```

will find where that lease was issued in
`Microsoft-Windows-Dhcp-Client%4Operational.evtx`
event ids 50058 / 50036
