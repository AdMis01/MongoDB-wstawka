# MongoDB-wstawka

### Podstawowe polecenia
Pokazywanie dostępnych baz danych
```
show dbs
```
Może też tworzyć lub zaznaczyć do korzystania bazy 
```
use []
```
Tworzy kolekcje
```
db.createCollection("")
```
Usuwanie bazy
```
db.dropDatabase()
```
Wyświetlanie danych
```
db.students.find() 
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
```
Wyszukiwanie na podstawie imienia
```
db.students.find({name: "Spange"})
```
Wyświetlanie tylko imion
```
db.students.find({}, {name: true})
```
### Modyfikowanie danych
Modyfikowanie pojedyńczych rekordów

- $set - ustawianie 
- $unset - usuwanie columny
- $exists - czy istnieje w danym stanie
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
$ne - not equal 
```
db.students.find({name: {$ne: "gary"}})
```
$lt - less then
```
db.students.find({age: {$lt: 20}})
```
$lte - less then and equal
```
db.students.find({age: {$lte: 20}})
```
$gt - greater then
```
db.students.find({age: {$gt: 20}})
```
$gte - greater then and equal
```
db.students.find({age: {$gte: 20}})
```
Można podać jeszcze wartości pomiędzy, przedział wartości
```
db.students.find({gpa: {$gte: 3,$lte: 4}})
```
$in - jeżeli wartość znajduje się w tablicy danych to wyświetli
```
db.students.find({name: {$in: ["sandy","patrik"]}})
```
$nin - not in jeżeli nie znajduje się w tablicy wartości to wyświetli
```
db.students.find({name: {$nin: ["sandy","patrik"]}})
```
$and - aby rekord musi spełniać oby dwa paremetry 
```
db.students.find({$and: [{fullTime: false}, {age: {$lte: 22}}]})
```
$or - or jeden z wymienionych elementów rekord musi spełniać 
```
db.students.find({$or: [{fullTime: false}, {age: {$lte: 22}}]})
```
$nor - kazde z nich musi byc fałszywe
```
db.students.find({$nor: [{fullTime: false}, {age: {$lte: 22}}]}) 
```
$nor - wyswietla ktore nie spełniaja warunku
```
db.students.find({age: {$not: {$gte: 30}}}) 
```
### Indeksowanie 
Tworzenie statusów indeksowania co pozwala na nieprzeszukiwanie całej 
```
db.students.find({name: "larry"}).explain("executionStats")
db.students.createIndex({name: 1})
```
Numer indeksu do wyszukiwania indeksów szybko
```
db.students.getIndexes()
db.students.dropIndex("name_1")
```
### Usuwanie kolecji/tablicy
```
show collections

db.createCollection("teachers", {capped: true, size: 10000000, max: 100}, {autoIndexId: false})
db.courses.drop()
```

