# MongoDB-wstawka

### Podstawowe polecenia
```
show dbs - pokazywanie dostępnych baz danych
use [] - może też tworzyć 
db.createCollection("") - tworzy kolekcje

db.dropDatabase() - usuwanie bazy
db.students.find() - wyświetlanie danych 
```
### Wstawianie wartości
```
db.students.insertOne({name: "imie", age: 30, gpa: 3.4})

db.studetns.insertOne({name: "Larry", age: 32, gpa: 2.8, fullTime: false, registerDate: new Date("2023-01-02T00:00:00"), gradutionDate: null, courses: ["bio","chem","cal"], address: {street: "elu", city: "pol"} })

db.students.insertMany([{name: "patrik", age: 38, gps: 1.5},{name: "sandy",age: 27, gpa: 4.0},{name: "gary", age: 18, gpa: 2.5}])
```
### Dodatkowe elementy 
- sort(1/-1) 
1 - alfabetyczne/najmiejsze
-1 - revers alfabetyczne/największego 
- limit(ilość ile się wyświetli)
```
db.students.find().sort(name: 1) alfabetycznie 
db.students.find().limit(1)
db.students.find({name: "Spange"})
db.students.find({}, {name: true})
```
### Modyfikowanie danych
Modyfikowanie pojedyńczych rekordów

$set - ustawianie 
```
db.students.updateOne({filter},{update})

db.students.updateOne({name: "Spange"}, {$set: {fullTime: true}})

db.students.updateOne({}, {$unset: {fullTime: ""}})
```
Modyfikowanie wielu danych
```
db.students.updateMany({},{$set:{fullTime: false}})

db.students.updateMany({name: "sandy"},{$unset:{fullTime: ""}})

db.students.updateMany({fullTime: {$exists: false}}, {$set:{fullTime: true}})
```
### Usuwanie

```
db.students.deleteOne({name: "larry"})

db.studetns.deleteMany({fullTime: false})

db.students.deleteMany({registerDate: {$exists: false}})
```
```
db.students.find({name: {$ne: "gary"}})

db.students.find({age: {$lt: 20}})

db.students.find({age: {$lte: 20}})

db.students.find({age: {$gt: 20}})

db.students.find({age: {$gte: 20}})

db.students.find({gpa: {$gte: 3,$lte: 4}})
```
```
db.students.find({name: {$in: ["sandy","patrik"]}})

db.students.find({name: {$nin: ["sandy","patrik"]}})

db.students.find({$and: [{fullTime: false}, {age: {$lte: 22}}]})

db.students.find({$or: [{fullTime: false}, {age: {$lte: 22}}]})

db.students.find({$nor: [{fullTime: false}, {age: {$lte: 22}}]}) - kazde z nich musi byc fałszywe

db.students.find({age: {$not: {$gte: 30}}}) wyswietla ktore nie spełniaja warunku

db.students.find({name: "larry"}).explain("executionStats")
db.students.createIndex({name: 1})
numer indeksu do wyszukiwania indeksów szybko

db.students.getIndexes()
db.students.dropIndex("name_1")

show collections

db.createCollection("teachers", {capped: true, size: 10000000, max: 100}, {autoIndexId: false})
db.courses.drop()
```

