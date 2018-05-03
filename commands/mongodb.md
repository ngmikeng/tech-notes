MongoDB Commands
===

## Mongo Import/Export
Import json data
- Import json data (type array) for database name `db1` into collection name `books` from file `~/dataImport.json`
- Optional params (--host 192.168.1.100 --port 27017) if want import from others host
```shell
$ mongoimport --db db1 --collection books --file ~/dataImport.json --jsonArray
```

Export json data
- Export to json data (type array) from database name `db1`, collection name `books`, out to file `~/dataExport.json`
- Optional params (--host 192.168.1.100 --port 27017) if want export from others host
```shell
$ mongoexport --db db1 --collection books --out ~/dataExport.json --jsonArray
```