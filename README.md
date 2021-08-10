# Commands
Commands needed for various tools 

# Mongodb Export dump and restore
First
* mongodump --db=old_db --collection=NERRules --out=F:\mongodump
 
then
* mongorestore --db=new_db --collection=NERRules "F:\mongodump\collection.bson"

