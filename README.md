# 📘 PLP Bookstore – MongoDB Fundamentals (Beginner Setup Guide)

This project introduces you to the fundamentals of MongoDB through hands-on practice. It includes inserting data, writing queries, using aggregation pipelines, and creating indexes for performance optimization.

---

## 🚀 Objective
By following this guide, you'll:
- Set up MongoDB on your machine (or use the cloud)
- Create a database and collection
- Insert book data
- Perform basic and advanced queries
- Use aggregations to summarize data
- Implement indexes to boost performance

---

## 🛠️ Prerequisites
You’ll need **one** of the following:

### Option A: Install MongoDB Locally
1. Visit: https://www.mongodb.com/try/download/community
2. Download MongoDB Community Edition
3. Install it (choose complete installation with MongoDB Compass)
4. Run the `mongosh` shell from terminal or Start menu

### Option B: Use MongoDB Atlas (Cloud)
1. Visit: https://www.mongodb.com/cloud/atlas
2. Create a free account
3. Deploy a free-tier cluster
4. Create a database user and allow access from all IP addresses
5. Connect via MongoDB Compass using the provided connection string

> MongoDB Compass is optional but highly recommended for beginners!

---

## 📂 Files Included
| File | Purpose |
|------|---------|
| `insert_books.js` | Optional Node.js script to insert data (advanced setup) |
| `queries.js` | Contains all MongoDB commands from Tasks 1–5 |
| `README.md` | This guide |
| `screenshots/` | Include Compass screenshots for visual proof |

---

## ⚙️ How to Setup and Run Queries

### Step 1: Launch the Shell
If using MongoDB locally, type:
```bash
mongosh
```

If using Atlas, connect using your provided connection string in MongoDB Compass.

---

### Step 2: Create the Database and Insert Books
Paste into shell:
```js
use plp_bookstore
```
Then paste the large array of book data from `insert_books.js` (or use Compass to insert documents).

---

## ✅ Task 2: Basic CRUD Operations

### 1. Find all books in a specific genre:
```js
db.books.find({ genre: "Adventure" })
```
> This finds all books where the genre is Adventure.

### 2. Find books published after a certain year:
```js
db.books.find({ published_year: { $gt: 1900 } })
```
> Finds all books published after 1900 using `$gt` (greater than).

### 3. Find books by a specific author:
```js
db.books.find({ author: "Paulo Coelho" })
```
> Matches all books by Paulo Coelho.

### 4. Update the price of a specific book:
```js
db.books.updateOne(
  { title: "Wuthering Heights" },
  { $set: { price: 15.99 } }
)
```
> Updates the price of "Wuthering Heights" to 15.99.

### 5. Delete a book by its title:
```js
db.books.deleteOne({ title: "Animal Farm" })
```
> Deletes one book titled "Animal Farm".

---

## ✅ Task 3: Advanced Queries

### 1. Books in stock and published after 2010:
```js
db.books.find({ in_stock: true, published_year: { $gt: 2010 } })
```

### 2. Return only title, author, price (projection):
```js
db.books.find({}, { title: 1, author: 1, price: 1, _id: 0 })
```

### 3. Sort books by price ascending:
```js
db.books.find().sort({ price: 1 })
```

### 4. Sort books by price descending:
```js
db.books.find().sort({ price: -1 })
```

### 5. Pagination – skip 5 books, get next 5:
```js
db.books.find().skip(5).limit(5)
```

---

## ✅ Task 4: Aggregation Pipelines

### 1. Average price by genre:
```js
db.books.aggregate([
  { $group: { _id: "$genre", avgPrice: { $avg: "$price" } } }
])
```
> Groups books by genre and calculates average price.

### 2. Author with most books:
```js
db.books.aggregate([
  { $group: { _id: "$author", bookCount: { $sum: 1 } } },
  { $sort: { bookCount: -1 } },
  { $limit: 1 }
])
```
> Finds the author with the highest number of books.

### 3. Group books by publication decade:
```js
db.books.aggregate([
  {
    $group: {
      _id: {
        $concat: [
          { $toString: { $multiply: [{ $floor: { $divide: ["$published_year", 10] } }, 10] } },
          "s"
        ]
      },
      count: { $sum: 1 }
    }
  }
])
```
> Calculates how many books were published per decade (e.g., 1980s).

---

## ✅ Task 5: Indexing & Performance

### 1. Create an index on title:
```js
db.books.createIndex({ title: 1 })
```
> Makes title searches faster.

### 2. Compound index on author and published_year:
```js
db.books.createIndex({ author: 1, published_year: -1 })
```
> Speeds up queries filtering by author and sorting by year.

### 3. Analyze performance using `.explain()`:
```js
db.books.find({ title: "The Hobbit" }).explain("executionStats")
```
> Look for `IXSCAN` (indexed) vs `COLLSCAN` (full collection scan).

---

## 📷 Screenshots Checklist
- [ ] Collection view in Compass (`books` with 12+ entries)
- [ ] Aggregation pipeline result (e.g., average by genre)
- [ ] Index tab showing your index fields
- [ ] Explain plan comparison before/after indexing

Save in a `screenshots/` folder and push to GitHub.

---

## ✅ Submission
Push the following to your GitHub Classroom repo:
- [x] `queries.js`
- [x] `README.md`
- [x] Screenshots folder

---

## 📚 MongoDB Resources
- Official Docs: https://www.mongodb.com/docs/manual/
- Aggregation Guide: https://www.mongodb.com/docs/manual/aggregation/
- Compass Download: https://www.mongodb.com/try/download/compass

---

You've now mastered the fundamentals of MongoDB. Good luck with the review!


## Resources

- [MongoDB Documentation](https://docs.mongodb.com/)
- [MongoDB University](https://university.mongodb.com/)
- [MongoDB Node.js Driver](https://mongodb.github.io/node-mongodb-native/) 
