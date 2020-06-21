# MongoDb CLI Commands

- [Manage databases](#manage-databases)
- [Manage Collections](#manage-collections)
- [Manage Documents](#manage-documents-in-collections)
- [Querying Data](#query-data-from-collections)



## Manage databases 

commands available to do operation with the dbs them self (without entering a db).



#### Shows in which db you are 

`db`  will simply return the name of the database 

#### Show available dbs

`show dbs` will return a list of dbs

#### Switch to a db

`use [db-name]` *if it doesn't exists will create one with the name provided*

#### Delete a db

`db.dropDatabase()` it's must be used inside the db it's gonna be deleted





## Manage Collections 

commands to manage collections once inside a db.



#### Show collections

`show collections`   shows all the already created collections in the db

#### Create a collection

`db.createCollection('collection-name')` the name must be a string

#### Delete a collection 

`db.[collection-name].drop()` 





## Manage documents in Collections 

manage data inside a collection. Can be inserted any kind of data : 

- Strings
- Numbers
- Arrays and Objects
- Date:  we can pass the current with the function `Date()` or a particular date `new Date("2020-12-01")`



#### Insert a document 

We use the command `db.[document-name].insert()` passing a Javascript like object .

```json
db.users.insert(
    {
        id:1,
        name:'john',  
        date: Date(),
      	todos: ['stuff', 'stuff', 'other stuff'],
      	moreInfo: {
          age: 35,
          lastName: 'Doe'
        }
    }
)
```



#### Insert multyple documents

we can create more than document at once using `db.product.insertMany()` passing an array of documents ( or objects ) as a json file.

```json
db.users.insertMany([ 
    {
        id:1,
        name:'john',  
        date: Date(),
        todos: ['stuff', 'stuff', 'other stuff'],
        moreInfo: {
          age: 35,
          lastName: 'Doe'
        }
    },
    {
        id:2,
        name:'Jason',  
        date: Date(),
        moreInfo: {
          dateOfBirth: new Date('01-25-1969')
        }
    }
])



```



#### Update documents 

will replace the entire documents using `db.[document-name].update({ parameter-of-search })` and passing as parameter an id of the document you wanna replace.

```json
db.users.update({id: 1},
    {
        id:1,
        name:'Jane',  
        date: Date(),
    }
)
```

create a new document if nothing matches with the parameter of the search passing `upsert: true`.

```json
db.users.update({id: 1},     
    {
        id:1,
        name:'Jane',  
        date: Date(),
    },
    {
    	upsert: true         
    }
)
```

replace a specific set of data inside the document using `{ $set:{...} }` , if nothing is passed it will create a new set.

```json
db.users.update({id: 1},       
    {
        $set: {                     
            name: 'jane'
        }
    }
)
```

increment number value in a data-set using `{ $inc:{...} }`.

```json
db.users.update({id: 1},       
    {
        $inc: {                     
            age: 3
        }
    }
)
```

rename a key in a key-value pair using `{ $rename:{...} }`.

```json
db.users.update({id: 1},       
    {
        $rename: {                     
            name: 'firstName'
        }
    }
)
```



#### Delete documents

Remove a document passing a search parameter using `db.[collection-name].remove({search-parameter}) `

```json
db.users.remove({ id: 1 }) 
```





## Query data from collections



#### Listing documents 

list all the documents in a specific collection `db.[collectio-name].find()`

```json
db.users.find()
```

format the documents when listing appending to the command `.pretty()`

```json                        
db.users.find().pretty()  
```

 Get data from a specific document  `.find({search-parameter})`

```json
db.users.find({ id: 2 }) 
```

sort the listed data by the key passed as parameter, `.find().sort({ parameter : 1 or -1 })` . `1` is for *crescent* order and `-1` for *decrescent* .

 ```json
db.users.find().sort({ name: 1 })

db.users.find().sort({ name: -1 }) 
 ```



#### Count and limits

count the number of documents in a collection `find().count()` .

```json
db.users.find().count() 
```

limit the number of documents listed in a search passing the number as parameter `.find().limit(limit)`

```json
db.users.find().limit(2) 
```

limit the number always to the first result `findOne()`

```json
db.users.findOne()
```



#### Advanced listing 

find documents using nested property as search paramenters ` $elemMatch:{...}`

```json
db.users.find({       
    moreInfo:{
        $elemMatch:{            
            age: 35
        }
    }
})
```

add custom behaviour when listing collections. `.find().forEach(item => print('stuff to log..') )`. *forEach* will loop through the listed data and will take a custom function. In this case will print something to the terminal for each document found. (print accept string interpolation or concatenation).

```json
db.users.find().forEach(document => {
  print('id' + document.id)
})

db.users.find().forEach(document => print(`id ${document.id}`))
```

list documents using *greater than* and *less than* :

- `$gt` greater than .
- `$gte` greater or equal than.
- `$lt` less than.
- `$lte` less or equal than.

```json
db.users.find({ age:{ $gt: 35 } })

db.users.find({ age:{ $lte: 35 } })
```



#### Indexing 

Will bind an index to a property of the document `.createIndex({ prop: order })` , the key in the parameter is the property we  want to get binded with an index,  the second is the order we want when querying.  With the value `1` will be *crescent* order, with `-1` decrescent .

```json 
db.users.createIndex({ id: 1 })

db.users.createIndex({ id: -1 })
```

Indexes can be bound. to other  types of data like *string* or *dates*.

```json
db.users.createIndex({ name: 1 })
```

Show the current indexes  `.getIndexes()`

```json
db.users.getIndexes()
```

Delete all the indexes `.dropIndexes()`

```json
db.users.dropIndexes()
```

Delete a specific index `.dropIndex(index-name: order)` , needs the name of the index and the order specified when created .

```json
db.users.dropIndex({name: 1})
```



