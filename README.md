# Commands
Commands needed for various tools 

# Mongodb Export dump and restore
First
* mongodump --db=old_db --collection=collection_name --out=F:\mongodump
 
then
* mongorestore --db=new_db --collection=collection_name "F:\mongodump\collection.bson"

