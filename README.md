# mongoDB-basics
## Table of Contents
- [Create DB, Collection](#create-collection)
- [Insert document](#insert-document)
- [Data Types](#datatypes)
- [Sorting and limiting](#sort-and-limit)
- [Find](#find)
- [Update Documents](#update-documents)
- [Delete Documents](#delete-documents)
- [Comparision](#comparision)
- [logical](#logical)
- [indexes](#indexes)
- [collection](#collections)

## Create Collection
show dbs - to show the databases.<br/>
use <db_name> - changes the DB also creates a new one if it doesn't exists. Example: use school<br/>
db.createCollection("collection_name") - creates a new collection. Example: db.createCollection("students")<br/>
db.dropDatabase - Deletes the DB<br/>

## Insert Document
db.students.insertOne({name:"Ajith", age:25, gpa:3.9}) - Inserts One doc<br/>
db.students.find() - Shows all docs<br/>
db.students.insertMany([{name:"Naveen", age:26, gpa:3.5},{name: "Sai", age:27, gpa:3.1},{name:"Sharath", age:28, gpa:2.9} ]) - Inserts multiple docs<br/>

## Datatypes
{<br/>
name: "Ajith" - String<br/>
age: 30 - Whole Number<br/>
gpa: 3.9 - Double<br/>
fullTime: false - Boolean<br/>
registerDate: new Date() - Current date and time <br/>
registerDate: new Date("2023-01-01T00:00:00") - Custom Date<br/>
graduationDate: null - Nulls which can be filled later<br/>
courses: ["Biology", "Chemistry", "Calculus"] - Array<br/>
address: {<br/>
          street: 123 Fake St,<br/>
          city: fake city<br/>
          }              - nested doc<br/>
}<br/>

## Sort and Limit
db.students.find().sort({name:1}) - sort takes a document. Sorting name in alphabetical order<br/>
db.students.find().sort({name:-1}) - reverse<br/>
db.students.find().limit(2) - takes integer to limit<br/>
db.students.find().sort({gpa:1}).limit(1) - Sort and limit<br/>

## Find
db.students.find() - All<br/>
db.students.find({query}, {projection}) - query is like Where condition and projection is like select condition<br/>
db.students.find({gpa:3.9}) - show who has gpa 3.9<br/>
db.students.find({gpa:3.9, fullTime:false}) - checks both conditions<br/>
db.students.find({_id: ObjectId("sixwqbxbxqwd1e32bie")}) - Finds by ID<br/>
db.students.find({}, {name:true}) - just get everybody's name<br/>
db.students.find({}, {_id:false, name:true}) - by default we get ID. So if we just want a name then make _id as false<br/>

## Update Documents
db.students.updateOne(filter, update) - filter is selection criteria, update is what to update<br/>
### Set
db.students.updateOne({name:"Ajith"}, {$set:{fullTime:false}}) - Pulls Ajith and sets fullTime as false. If that field is not present then adds a new one<br/>
db.students.updateOne({_id: ObjectId("3e9h93wf8q3f")}, {$set:{fullTime:false}}) - Update based on ObjectId<br/>
### unset
db.students.updateOne({_id: ObjectId("vewbic3d91dewc")}, {$unset:{fullTime:""}}) - it will remove the value and also the field <br/>
db.students.updateMany({},{$set:{fullTime:false}}) - set fullTime to false for all<br/>
### exists
db.students.updateMany({fullTime:{$exists:false}}, {$set:{fullTime:true}}) - If any student doesn't have fullTime field then add it<br/>


## Delete Documents
db.students.deleteOne(filter) - filter criteria<br/>
db.students.deleteOne({name:"Ajith"}) - Doc with name as Ajith will be deleted<br/>
db.students.deleteMany({fullTime:false}) - Doc with fullTime as false will be deleted<br/>
db.students.deleteMany({registerDate:{$exists:false}}) - Docs without registerDate field will be deleted<br/>

## Comparision
### ne - Not equals
db.students.find({name:{$ne:"Ajith"}}) - returns all docs which doesn't have name as Ajith<br/>
### lt, lte - lessthan & lessthan equal to
db.students.find({age:{$lt:27}})<br/>
db.students.find({age:{$lte:27}})<br/>
db.students.find({age:{$gt:27}})<br/>
db.students.find({age:{$gte:27}})<br/>

db.students.find({gpa:{$gte:3, $lte:3.9}}) - both lessthan and greaterthan<br/>
### in & nin - IN and Not IN
db.students.find({name:{$in:["Ajith", "Sai"]}}) - Returns docs with names in arrays<br/>

## Logical
### And
db.students.find({$and: [{fullTime:true}, {age:{$lte:22}}]}) - And condition to check both <br/>
Similarly we have OR and NOR <br/>
db.students.find({$or: [{fullTime:true}, {age:{$lte:22}}]}) <br/>
db.students.find({$nor: [{fullTime:true}, {age:{$lte:22}}]}) - Both should be false <br/>
### Not
db.students.find({age:{$not:{$gte:30}}}) - Additional benifit is, it returns nulls too. So students which age as null will also be returned <br/>


## Indexes
Allow for a quick look up of field but it take more memory and slows insert and update operation. Use wisely<br/>
### Execution Stats
db.students.find({name:"Ajith"}).explain("executionStat") - Gives the execution stats of a query <br/>
### Create Index
db.students.createIndex({name:1}) - 1 in Asc order and -1 for desc order <br/>
### Get Index
db.students.getIndexes()<br/>
### Drop Index
db.students.dropIndex("Index_Name")<br/>


## Collections
show collections - shows the collections<br/>
db.createCollection("teahcer") - just creates a collection<br/>  
db.createCollection("teacher", , {capped:true, size:1000000, max:100}) - If capped is true then we say to mongoDb that this collection has a maximum size.
If capped is set to true then we have to set max size or max documents <br/>
db.createCollection("teacher", , {capped:true, size:1000000, max:100}, {autoIndexId:true}) - Automatically we apply an index to Object Ids. <br/>
db.teacher.drop() - drop a collection<br/>





