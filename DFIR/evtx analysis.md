> EVTX is a binary file format used by Windows for storing event logs. It replaces the older .evt format, offering features like a structured XML format, improved event properties, and more efficient storage. 

Tools:
- [chainsaw](https://github.com/WithSecureLabs/chainsaw?tab=readme-ov-file#quick-start-guide)
- [hayabusa](https://github.com/Yamato-Security/hayabusa)


Can upload to [Gigasheet](https://app.gigasheet.com/datasets) for free CSV parsing

# chainsaw
search for specific event id
```
chainsaw search -t 'Event.System.EventID: =XXXX' <evtx_file_path>
```

Running rule lists against .evtx files
```
chainsaw hunt <file.evtx> --sigma <path>chainsaw/sigma/rules/windows --mapping <path>/chainsaw/mappings/sigma-event-logs-all.yml
```

extracting events to json
```
chainsaw dump /path/file.evtx --output /path/output.json -j
```


---
# hayabusa
```
./hayabusa csv-timeline -f "file.evtx" -o "timeline.csv"
```