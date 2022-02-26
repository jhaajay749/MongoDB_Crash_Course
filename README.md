# MongoDB_Crash_Course


/////////////////////////////////////////////////////////////////////////////////////////

 mongo

>show dbs

>use test1

>show collections

>db.dropDatabase()

>show dbs

>use acme

>db

>db.createCollection("posts")

>show collections

>db.posts.insert({
       title: "Post One",
       body:  "Body of post one",
       category: "News",
       likes: 4,
       tags: ["news", "events"],
       user:{
         name: "Ajay Kumar Jha",
         status: "developer"
       },
       date: Date()
});

>db.posts.insertMany([
  {
    title: "Post Two",
    body: "Body of post two",
    category: "Technology",
    date: Date()
  },
  {
    title: "Post Three",
    body: "Body of post three",
    category: "Science",
    date: Date()
  },
  {
    title: "Post Four",
    body: "Body of post two",
    category: "information technology",
    date: Date()
  }

]);

>clear - ctrl + l

>db.posts.find()

>db.posts.find().pretty()

>db.posts.find({category: "News"})

>db.posts.find({category: "News"}).pretty()

>db.posts.find().sort({title: 1}).pretty()

>db.posts.find({category: "News"}).count()

>db.posts.find().limit(2)

>db.posts.find().sort({title: -1}).limit(2)

>db.posts.find().forEach(function(doc){print("Blog Post: " + doc.title)})

>db.posts.findOne({category: "News"})

>db.posts.update({title: "Post Two"},
  {
    title: "Post Two",
    body:  "New post 2 body",
    date:  Date()
  },
  {
    upsert: true
  }
)


>db.posts.find({title: "Post Two"}).pretty()

>db.posts.update({title: "Post Two"},
 {
   $set:{
       body: "Body of post 2",
       category: "Technology"
   }
 }
)


>db.posts.update({title: "Post One"}, {$inc: {likes: 2}})

>db.posts.update({title: "Post One"}, {$rename: {likes: "views"}})

>db.posts.remove({title: "Post Four"})

>db.posts.update({title: "Post One"},
 {
    $set:{
         comments: [
                {
                  user: "Mary Williams",
                  body: "Comment One",
                  date: Date()
                },
                {
                  user: "Harry White",
                  body: "Comment Two",
                  date: Date()
                }
            ]
     }
 }
)

>db.posts.find({
   comments:{
       $elemMatch:{
         user: "Mary Williams"
       }
   }
}).pretty()


>db.posts.createIndex({title: "text"})

>db.posts.find({
   $text:{
      $search: "\"Post O\""
   }
}).pretty()


>db.posts.find({
   $text:{
      $search: "\"Post T\""
   }
}).pretty()

>db.posts.update({title: "Post Two"}, {$set: {views: 10}})

>db.posts.find({views: {$gt:3}}).pretty()

>db.posts.find({views: {$gte:3}}).pretty()

>db.posts.find({views: {$lte:6}}).pretty()

>exit


/////////////////////////////////////////////////////////
// When Mongo shell connected to MongoDB Atlas

>show dbs

>use acme

>db.createCollection("todos")

>db.todos.insert({text: "Todo One"})

>db.todos.find().pretty()


/////////////////////////////////////////////////////////////////

MongoDB Cheat Sheet

///////////////////////////////
Show All Databases

>show dbs

//////////////////////////////
Show Current Database

>db

////////////////////////////
Create Or Switch Database
>use acme

//////////////////////////
Drop
>db.dropDatabase()

/////////////////////////
Create Collection
>db.createCollection('posts')

/////////////////////////
Show Collections
>show collections

///////////////////////
Insert Row
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})

///////////////////////////
Insert Multiple Rows
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

/////////////////////////
Get All Rows
db.posts.find()

/////////////////////////
Get All Rows Formatted
db.posts.find().pretty()

/////////////////////////
Find Rows
db.posts.find({ category: 'News' })

////////////////////////
Sort Rows
# asc
db.posts.find().sort({ title: 1 }).pretty()
# desc
db.posts.find().sort({ title: -1 }).pretty()

////////////////////////
Count Rows
db.posts.find().count()
db.posts.find({ category: 'news' }).count()

///////////////////////
Limit Rows
db.posts.find().limit(2).pretty()

//////////////////////
Chaining
db.posts.find().limit(2).sort({ title: 1 }).pretty()

/////////////////////
Foreach
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})

/////////////////////
Find One Row
db.posts.findOne({ category: 'News' })
Find Specific Fields
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})

/////////////////////
Update Row
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})

///////////////////////////////////////
Update Specific Field
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})

//////////////////////////////////
Increment Field ($inc)
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})

/////////////////////////////////////
Rename Field
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})

////////////////////////////////////////
Delete Row
db.posts.remove({ title: 'Post Four' })
Sub-Documents
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})

////////////////////////////////////////////
Find By Element in Array ($elemMatch)
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)


///////////////////////////////////////////
Add Index
db.posts.createIndex({ title: 'text' })

//////////////////////////////////////////
Text Search
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
})

///////////////////////////////////////////
Greater & Less Than
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })






