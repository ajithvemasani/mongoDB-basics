# mongoDB-basics
## Table of Contents
- [Create DB, Collection](#create-collection)
- [Insert document](#insert-document)
- [Data Types](#datatypes)
- [Sorting and limiting](#sort-and-limit)
- [Find](#find)
- [Update Documents](#update-documents)
- [Delete Documents](#delete-documents)

## Create Collection
show dbs - to show the databases.
use <db_name> - changes the DB also creates a new one if it doesn't exists. Example: use school
db.createCollection("collection_name") - creates a new collection. Example: db.createCollection("students")
db.dropDatabase - Deletes the DB

## Insert Document
db.students.insertOne({name:"Ajith", age:25, gpa:3.9}) - Inserts One doc
db.students.find() - Shows all docs
db.students.insertMany([{name:"Naveen", age:26, gpa:3.5},{name: "Sai", age:27, gpa:3.1},{name:"Sharath", age:28, gpa:2.9} ]) - Inserts multiple docs

## Datatypes
{
name: "Ajith" - String
age: 30 - Whole Number
gpa: 3.9 - Double
fullTime: false - Boolean
registerDate: new Date() - Current date and time 
registerDate: new Date("2023-01-01T00:00:00") - Custom Date
graduationDate: null - Nulls which can be filled later
courses: ["Biology", "Chemistry", "Calculus"] - Array
address: {
          street: 123 Fake St,
          city: fake city
          }              - nested doc
}

## Sort and Limit
db.students.find().sort({name:1}) - sort takes a document. Sorting name in alphabetical order
db.students.find().sort({name:-1}) - reverse
db.students.find().limit(2) - takes integer to limit
db.students.find().sort({gpa:1}).limit(1) - Sort and limit

## Find
db.students.find() - All
db.students.find({query}, {projection}) - query is like Where condition and projection is like select condition
db.students.find({gpa:3.9}) - show who has gpa 3.9
db.students.find({gpa:3.9, fullTime:false}) - checks both conditions
db.students.find({_id: ObjectId("sixwqbxbxqwd1e32bie")}) - Finds by ID
db.students.find({}, {name:true}) - just get everybody's name
db.students.find({}, {_id:false, name:true}) - by default we get ID. So if we just want a name then make _id as false

## Update Documents
db.students.updateOne(filter, update) - filter is selection criteria, update is what to update
### Set
db.students.updateOne({name:"Ajith"}, {$set:{fullTime:false}}) - Pulls Ajith and sets fullTime as false. If that field is not present then adds a new one
db.students.updateOne({_id: ObjectId("3e9h93wf8q3f")}, {$set:{fullTime:false}}) - Update based on ObjectId
### unset
db.students.updateOne({_id: ObjectId("vewbic3d91dewc")}, {$unset:{fullTime:""}}) - it will remove the value and also the field 
db.students.updateMany({},{$set:{fullTime:false}}) - set fullTime to false for all
### exists
db.students.updateMany({fullTime:{$exists:false}}, {$set:{fullTime:true}}) - If any student doesn't have fullTime field then add it


## Delete Documents
db.students.deleteOne(filter) - filter criteria
db.students.deleteOne({name:"Ajith"}) - Doc with name as Ajith will be deleted
db.students.deleteMany({fullTime:false}) - Doc with fullTime as false will be deleted
db.students.deleteMany({registerDate:{$exists:false}}) - Docs without registerDate field will be deleted


