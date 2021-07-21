# MongoDB Cheat Sheet

## Show All Databases

```
show dbs
```

## Show Current Database

```
db
```

## Create Or Switch Database

```
use name-of-db
```

## Drop Database

```
db.dropDatabase()
```

## Create Collection

```
db.createCollection('name-of-collection')
```

## Show Collections

```
show collections
```



=== we are going to work with a collection "posts" as an example ===


## Insert Row
It is like a js object. you can pass everything there even js methods

```
db.posts.insert({
  title: 'Title One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

## Insert Multiple Rows

```
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```

## Get All Rows

```
db.posts.find({})
```

## Get All Rows Formatted

```
db.posts.find().pretty()
```

## Find Rows

```
db.posts.find({ row-name-key: 'row-name' })
```

## Sort Rows
in most cases you want to find by ID

```
# asc
db.posts.find().sort({ row-name-key: identifier }).pretty()
# desc
db.posts.find().sort({ row-name-key: -identifier }).pretty()
```

## Count Rows

```
db.posts.find().count()
db.posts.find({ category: 'news' }).count()
```

## Limit Rows
how many posts to show

```
db.posts.find().limit(2).pretty()
```

## Foreach
! a function takes a param

```
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

## Find One Row

```
db.posts.findOne({ category: 'News' })
```

## Find Specific Fields

```
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})
```

## Update Row
! if we are not updating with a $set, a row is going to have exact props that you "updated". Parms that you did not mention are going to be deleted from row

```
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

## Update Specific Field
! Fields that are not mentioned are going to stay the same (not as in prev rule)

```
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'WebDev'
  }
})
```

## Rename Field
1) Specifing a fild that we wanna change, u probably wanna select it by ID
2) Use $rename
```
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

## Delete Row

```
db.posts.remove({ title: 'Post Four' })
```

## Sub-Documents

```
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'John Doe',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Jane Doe',
        date: Date()
      }
    ]
  }
})
```

## Find By Element in Array (\$elemMatch)

```
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'John Doe'
       }
    }
  }
)
```

## Add Index

```
db.posts.createIndex({ title: 'text' })
```

## Greater & Less Than

```
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```

