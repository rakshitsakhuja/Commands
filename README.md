# Commands
Commands needed for various tools 

# Mongodb Export dump and restore
First
* mongodump --db=ProdSLBConfig --collection=NERRules --out=F:\mongodump
 
then
* mongorestore --db=SLBConfig_Cognitive --collection=NERRules "F:\mongodump\collection.bson"

