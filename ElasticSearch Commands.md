# Restore and backup data in elasticsearch

### Step 1 
1. register a snapshot in the elasticsearch system where we need to take backup from

* Before the below step , mention the location in path.repo in elasticsearch.yml file as path.repo:["/backup_snapshot"]
* Restart the elasticsearch service
* Register Snapshot

```
PUT /_snapshot/es_backup
{
  "type": "fs",
  "settings": {
    "location": "/backup_snapshot"
  }
}
```
* Create Snapshot
```
PUT /_snapshot/es_backup/snapshot_2?wait_for_completion=true
{
  "indices": "index1,index2,
  "ignore_unavailable": true,
  "include_global_state": false,
  "metadata": {
    "taken_by": "rakshit",
    "taken_because": "copying to diff server"
  }
}
```
### Step 2
* Paste the snapshot files from backup directory to server where you need to restore the backup
* Mention the backup directory in path.repo of elasticsearch.yml where you are pasting files
* Restart the server
* Register the snapshot
 
```
PUT /_snapshot/es_backup
{
  "type": "fs",
  "settings": {
    "location": "/backup_snapshot"
  }
}
```
* Restore the backup
```
POST /_snapshot/es_backup/snapshot_2/_restore
{
  "indices": "index1,index2",
    "ignore_unavailable": true,
  "include_global_state": false,              
  "rename_pattern": "index_(.+)",
  "rename_replacement": "restored_index_$1",
  "include_aliases": false

}
```

```
POST /_snapshot/es_backup/snapshot_2/_restore
```




