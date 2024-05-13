use pruthvi;

db.students.insertOne({name:"Pruthvi",usn:"scs14",branch:"cse",dept:"cs",address:"hebbal",age:22})

db.students.find()

db.students.insertMany([{name:"harsha",usn:"scs05",branch:"cse",dept:"cs",address:"hassan",age:23},{name:"Sanjith",usn:"scs16",branch:"cse",dept:"cs",address:"RV",age:22},{name:"Hrishikesh",usn:"scs09",branch:"cse",dept:"cs",address:"abbigere",age:22},{name:"Jayanth",usn:"scs13",branch:"cse",dept:"cs",address:"BEL",age:22},{name:"Neeraj",usn:"scn02",branch:"cne",dept:"cs",address:"ooru",age:22},{name:"Tresa",usn:"scs03",branch:"cse",dept:"cs",address:"Yehlanka",age:21},{name:"Jayanth",usn:"scn05",branch:"cne",dept:"cs",address:"hassan",age:22}])

db.students.find({branch:"cne"})

db.students.updateOne({usn:"pgcs15"},{$set:{age:23}})

db.students.updateMany({branch:"cne"},{$set: {dept:"cn"}})

db.students.find({branch:"cne"})

db.students.deleteOne({name:"Pruthvi"})

db.students.find()

db.students.aggregate([{$match:{dept:"cs"}},{$count:"Total students in CSE dept"}])

db.students.aggregate([{$match:{dept:"cn"}},{$count:"Total students in CNE dept"}])

db.students.aggregate([{$match:{age:{$gt:22}}}])

db.students.find().sort({usn:1})

db.students.createIndex({age:1})

db.students.getIndexes()

db.students.find().hint({age:1})

db.students.dropIndex({age:1})

db.students.aggregate([{$match:{age:{$gt:20}}},{$limit:2}])
