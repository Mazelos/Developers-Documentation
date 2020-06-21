# MongoDb CLI Commands

- [Manage databases](#manage-databases)

- [Manage Collections](#manage-collections)

    - [Show collections](#show-collections)
    - [Create collections](#create-a-collection)
    - [Delete collections](#delete-a-collection)
    
- [Manage Documents](#manage-documents-in-collections)

    - [Insert a Document](#insert-a-document)
    - [Insert multyple Documents](#insert-multyple-documents)
    - [Update Documents](#update-documents)
    - [Delete Documents](#delete-documents)
    
- [Querying Data](#query-data-from-collections)
    
    - [Listing documents](#listing-documents)
    - [Count and limits](#count-and-limits)
    - [Advanced listing](#advanced-listing)
    - [Indexing](#indexing)
    
</br>
</br>

# Manage databases 

commands available to do operation with the dbs them self (without entering a db).
</br>

## Shows in which db you are 

`db`  will simply return the name of the database 

## Show available dbs

`show dbs` will return a list of dbs

## Switch to a db

`use [db-name]` *if it doesn't exists will create one with the name provided*

## Delete a db

`db.dropDatabase()` it's must be used inside the db it's gonna be deleted


</br></br>



# Manage Collections 

commands to manage collections once inside a db.



## Show collections

`show collections`   shows all the already created collections in the db

## Create a collection

`db.createCollection('collection-name')` the name must be a string

## Delete a collection 

`db.[collection-name].drop()` 

</br>
</br>



# Manage documents in Collections 

manage data inside a collection. Can be inserted any kind of data : 

- Strings
- Numbers
- Arrays and Objects
- Date:  we can pass the current with the function `Date()` or a particular date `new Date("2020-12-01")`



## Insert a document 

We use the command `db.[document-name].insert()` passing a Javascript like object .

```
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



## Insert multyple documents

we can create more than document at once using `db.product.insertMany()` passing an array of documents ( or objects ) as a json file.

```
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



## Update documents 

will replace the entire documents using `db.[document-name].update({ parameter-of-search })` and passing as parameter an id of the document you wanna replace.

```
db.users.update({id: 1},
    {
        id:1,
        name:'Jane',  
        date: Date(),
    }
)
```

create a new document if nothing matches with the parameter of the search passing `upsert: true`.

```
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

```
db.users.update({id: 1},       
    {
        $set: {                     
            name: 'jane'
        }
    }
)
```

increment number value in a data-set using `{ $inc:{...} }`.

```
db.users.update({id: 1},       
    {
        $inc: {                     
            age: 3
        }
    }
)
```

rename a key in a key-value pair using `{ $rename:{...} }`.

```
db.users.update({id: 1},       
    {
        $rename: {                     
            name: 'firstName'
        }
    }
)
```



## Delete documents

Remove a document passing a search parameter using `db.[collection-name].remove({search-parameter}) `

```
db.users.remove({ id: 1 }) 
```

</br>
</br>



# Query data from collections


## Listing documents 

list all the documents in a specific collection `db.[collectio-name].find()`

```
db.users.find()
```

format the documents when listing appending to the command `.pretty()`

```                       
db.users.find().pretty()  
```

 Get data from a specific document  `.find({search-parameter})`

```
db.users.find({ id: 2 }) 
```

sort the listed data by the key passed as parameter, `.find().sort({ parameter : 1 or -1 })` . `1` is for *crescent* order and `-1` for *decrescent* .

 ```
db.users.find().sort({ name: 1 })

db.users.find().sort({ name: -1 }) 
 ```



## Count and limits

count the number of documents in a collection `find().count()` .

```
db.users.find().count() 
```

limit the number of documents listed in a search passing the number as parameter `.find().limit(limit)`

```
db.users.find().limit(2) 
```

limit the number always to the first result `findOne()`

```
db.users.findOne()
```



## Advanced listing 

find documents using nested property as search paramenters ` $elemMatch:{...}`

```
db.users.find({       
    moreInfo:{
        $elemMatch:{            
            age: 35
        }
    }
})
```

add custom behaviour when listing collections. `.find().forEach(item => print('stuff to log..') )`. *forEach* will loop through the listed data and will take a custom function. In this case will print something to the terminal for each document found. (print accept string interpolation or concatenation).

```
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

```
db.users.find({ age:{ $gt: 35 } })

db.users.find({ age:{ $lte: 35 } })
```



## Indexing 

Will bind an index to a property of the document `.createIndex({ prop: order })` , the key in the parameter is the property we  want to get binded with an index,  the second is the order we want when querying.  With the value `1` will be *crescent* order, with `-1` decrescent .

```
db.users.createIndex({ id: 1 })

db.users.createIndex({ id: -1 })
```

Indexes can be bound. to other  types of data like *string* or *dates*.

```
db.users.createIndex({ name: 1 })
```

Show the current indexes  `.getIndexes()`

```
db.users.getIndexes()
```

Delete all the indexes `.dropIndexes()`

```
db.users.dropIndexes()
```

Delete a specific index `.dropIndex(index-name: order)` , needs the name of the index and the order specified when created .

```
db.users.dropIndex({name: 1})
```



