# Commands
Commands needed for various tools 

# MongoDB

## Mongodb Export dump and restore
First
* mongodump --db=old_db --collection=collection_name --out=F:\mongodump
 
then
* mongorestore --db=new_db --collection=collection_name "F:\mongodump\collection.bson"

In case of Authentication
*  mongorestore -u rakshit -p rakshit --authenticationDatabase admin --collection="collection_name"  --db="new_db"  "F:\mongodump\collection.bson"

## Convert BSON to csv

* bsondump collection.bson > file.csv
## Add column in Mongodb in collection for all documents

db.collection_name.updateMany({},{$set:{'col_name':''}})

## Delete column in Mongodb in collection for all documents

db.collection_name.updateMany({},{$unset:{'col_name':''}})

## Authentication in MongoDB
https://www.youtube.com/watch?v=bZhlX90m1cw 

https://docs.anaconda.com/anaconda-repository/admin-guide/install/config/config-mongodb-authentication/

1. mongosh
2. use admin
3. db.createUser({user:'rakshit', pwd: 'rakshit', roles:["userAdminAnyDatabase","dbAdmin","readWrite","root"]})
     * root = will allow you to create read update all tables
     * userAdminAnyDatabase = will allow you to create users
     * dbAdmin
     * readWrite = will give you permision to read write any table

4. db.auth('rakshit', 'rakshit')

5. Paste below code in /etc/mongod.conf
      * security:
      *    authorization: enabled
6. sudo service mongod restart
7. mongosh -u rakshit -p rakshit
