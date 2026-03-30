Content Management System (CMS) - MongoDB Project

This project demonstrates MongoDB operations using a Content Management System (CMS) dataset including users, posts, and comments.

---

## 📌 Features

- Database and collection creation  
- CRUD operations (Create, Read, Update, Delete)  
- Filtering and projection  
- View creation  
- Schema validation using JSON Schema  

---
```js
🗄️ Create Database
db.use("cmsDB")
📁 Create Collections
db.createCollection("users")
db.createCollection("posts")
db.createCollection("comments")
➕ Insert Operation
db.users.insertOne({
  username: "arun123",
  email: "arun@gmail.com",
  role: "admin",
  age: 21,
  isActive: true
})
db.posts.insertOne({
  title: "Introduction to MongoDB",
  category: "Technology",
  author: "arun123",
  views: 100,
  postId: "POST1001"
})
📖 Read Operation
db.users.find().pretty()
db.posts.find().pretty()
🔍 Filter
db.posts.find({ category: "Technology" })
db.posts.find({ views: { $gt: 50 } })
📌 Projection
db.users.find({}, { username: 1, email: 1, _id: 0 })
✏️ Update
db.users.updateOne(
  { username: "arun123" },
  { $set: { role: "editor" } }
)
db.posts.updateMany(
  { category: "Technology" },
  { $inc: { views: 10 } }
)
❌ Delete
db.users.deleteOne({ username: "arun123" })
db.posts.deleteMany({ views: { $lt: 50 } })
👁️ View
db.createView(
  "techPosts",
  "posts",
  [
    { $match: { category: "Technology" } }
  ]
)
✅ Validation
Users Collection Validation
db.createCollection("users_validation", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["username", "email", "role"],
      properties: {
        username: { bsonType: "string" },
        email: { bsonType: "string" },
        role: { bsonType: "string" },
        age: { bsonType: ["int", "null"] },
        isActive: { bsonType: "bool" }
      }
    }
  }
})
Posts Collection Validation (Advanced)
db.createCollection("posts_validation", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["title", "category", "author", "views"],
      properties: {
        title: {
          bsonType: "string",
          minLength: 5,
          maxLength: 150
        },
        category: {
          enum: ["Technology", "Education", "Lifestyle", "News"]
        },
        author: {
          bsonType: "string"
        },
        views: {
          bsonType: "int",
          minimum: 0
        },
        postId: {
          bsonType: ["string", "null"],
          pattern: "^POST[0-9]{4}$"
        }
      }
    }
  },
  validationLevel: "strict",
  validationAction: "error"
})
📸 Screenshots
All outputs are available in the screenshots folder.
📊 Conclusion
This project demonstrates CRUD operations, filtering, projection, view creation, and schema validation using MongoDB in a CMS environment.
