# Learned Basics of MongoDB

Below are the commands that are documented and applied on a students DB which is present in form of csv file in repo

MONGO DB:

1. show dbs
# To show db

2. use admin

3. use school
# To create a school db

4. db.createCollection("students")
# Run the above cmd in school db and now use show dbs to view school db which was created earlier 

5. db.dropDatabase()
# Deletes the db and no longer appears in show dbs

Similar cmds listed above can be done in GUI using MongoDB Compass

6. db.students.insertOne({name:"Spongebob", age:30, gpa:3.2})
# Creates a document in the students collection

7. db.students.find()
# To find the documents in the collection 

8. db.students.insertMany([{name:"Patrick", age:38, gpa:1.5},{name: "Sandy", age:27, gpa:4.0},{name:"Gary", age:18, gpa:2.5}])
# To insert multiple documents in the collection

Similar cmds listed above can be done in GUI using MongoDB Compass

9. db.students.insertOne({name:"Pavan", age: 32, gpa: 2.8, fullTime: false,
							registerDate: new Date(), gradDate: null,
							courses: ["Biology", "Chemistry", "Calculas"],
							address: {street:"133 South Park St", city: "Hlifax", zip: 12345}})
# Datatypes in MongoDB
					
10. db.students.find().sort({name:1})
# Sort names - 1 by alphabetical order or ascending and names - (-1) for reverse alphabetical order or descending

11. db.students.find({name: "Spongebob"})
# To search for a specific document also can be used to search multiple documents

12. db.students.find({},{name:true})
# This is projection paramater in MongoDB which returns only the name in the documents along with Id's

13. db.students.find({},{_id:false, name:true})
# This is projection paramater in MongoDB which returns only the name in the documents with no Id's

14. db.students.find({},{_id:false, name:true, gpa:true})
# This is projection paramater in MongoDB which returns only the name in the documents with no Id's along with gpa's

15. db.students.updateOne({name:"Sandy"}, {$set:{fullTime:true}})
# Update document with name followed by the fulltime feild

16. db.students.updateOne({_id:ObjectId("647bf6f9ed841d93b4b95153")}, {$set:{fullTime:false}})
# Update document with name followed by the fulltime feild using Id's which is a best practise

17. db.students.updateOne({_id:ObjectId("647bf6f9ed841d93b4b95153")}, {$unset:{fullTime:""}})
# Update document with name followed by the removing feild using Id's which is a best practise

18. db.students.updateMany({}, {$set:{fullTime:true}})
# Update multiple documents with name followed by the fulltime feild

19. db.students.updateMany({fullTime:{$exists:false}}, {$set:{fullTime:true}})
# Update multiple documents who dont have a full time feild then update with fulltime 

20. db.students.deleteOne({name:"Gary"})
# Delete a document with name

21. db.students.deleteMany({fullTime:false})
# Delete multiple documents with fulltime

22. db.students.deleteMany({registerDate:{$exists:false}})
# Delete multiple documents if the registerDate feild doesn't exists

23. db.students.find({name:{$ne:"Spongebob"}})
# This Not Equal to operator in MongoDB which returns values other than Spongebob

24. db.students.find({age:{$lt:20}})
# This Less than to operator in MongoDB which returns values of age less than 20

25. db.students.find({age:{$lte:27}})
# This Less than or Equal to operator in MongoDB which returns values of age less than or equal to 27

26.db.students.find({age:{$gt:20}})
# This Greater than to operator in MongoDB which returns values of age greater than 20

27. db.students.find({age:{$gte:27}})
# This Greater than or Equal to operator in MongoDB which returns values of age greater than or equal to 27

28. db.students.find({age:{$gte:27, $lte:4}})
# Multiple Comparision Operators

29. db.students.find({name:{$in:["Spongebob","Pavan"]}})
# This is a IN operator in MongoDB which returns values where on of this values in array is found with name feild

30. db.students.find({name:{$nin:["Spongebob","Pavan"]}})
# This is a NOT-IN operator in MongoDB which doesn't returns values where on of this values in array is found with name feild

31. db.students.find({$and: [{fullTime:true}, {age:{$lte:38}}]})
# This is a conditional AND Operator with multiple conditions in it

32. db.students.find({$or: [{fullTime:true}, {age:{$lte:38}}]})
# This is a conditional OR Operator with multiple conditions in it

33. db.students.find({$nor: [{fullTime:true}, {age:{$lte:38}}]})
# This is a conditional NOR Operator with multiple conditions in it , both false

34. db.students.find({age:{$not:{$gte:30}}})
# This is a conditional NOT Operator which returns ages less than 30 even if any age has NULL feild

35. Indexes: Allows for quick look of feild which takes memory slows Insert, Update, and Remove operations

	db.students.find({name:"Garry"}).explain("executionStats") 
# We have examined all documents present in collection to find Garry in a Linear Search
	
# Say suppose we have 1000's of documents than it going to take lot of time so we use index here
	
36. db.students.createIndex({name: 1})
# Create a index and arrage data using ascending 1 or descending -1
	
37.	db.students.find({name:"Garry"}).explain("executionStats") 
# Now check the value "docsExamined" which reduces from earlier case
	
38.	db.students.getIndexes()
# To view indexes
	
39.	db.students.dropIndex("name_1")
# To drop Index 
	
40. Collection is a group of Documents
	Database is group of Collections
	
	show collections
# Views the list of collections
	
41. db.createCollection("teachers")
# To create collection
	
42. db.createCollection("teachers", {capped:true, size:1000000, max:100})
# To create collection with max size 10MB and max documents

42. db.createCollection("teachers", {capped:true, size:1000000, max:100}, {autoIndexId: false)
# To create collection with max size 10MB and max collections with no indexes

43. db.<collection-name>.drop()
# Drop collection-name
