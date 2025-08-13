> EVTX is a binary file format used by Windows for storing event logs. It replaces the older .evt format, offering features like a structured XML format, improved event properties, and more efficient storage. 

Tools:
- chainsaw
- hayabusa


Can upload to [Gigasheet](https://app.gigasheet.com/datasets) for free CSV parsing

# chainsaw
search for specific event id
```
chainsaw search -t 'Event.System.EventID: =XXXX' <evtx_file_path>
```

Running rule lists against .evtx files
```
chainsaw hunt <file.evtx> --sigma /<pat>chainsaw/sigma/rules/windows --mapping /Users/jaswal1/tools/chainsaw/mappings/sigma-event-logs-all.yml
```