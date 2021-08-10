# Commands
Commands needed for various tools 

# MongoDB

## Mongodb Export dump and restore
First
* mongodump --db=old_db --collection=collection_name --out=F:\mongodump
 
then
* mongorestore --db=new_db --collection=collection_name "F:\mongodump\collection.bson"

## Convert BSON to csv

* bsondump collection.bson > file.csv

