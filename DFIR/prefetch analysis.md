making timeline using log2timeline
```sh
log2timeline --parsers prefetch --storage_file timeline.plaso .
```
build csv
```sh
psort -o l2tcsv -w prefetch.csv timeline.plaso
```