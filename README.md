<img src="https://socialify.git.ci/Bongeka-Bhungane/Library-Management-System/image?description=1&font=Raleway&language=1&name=1&owner=1&pattern=Circuit+Board&theme=Light" alt="Library-Management-System" width="640" height="320" />

#Library Management System (PostgreSQL)

## 🧾 Project Overview
This project is a **Library Management System** built using **PostgreSQL**.  
It allows managing books, authors, and patrons through SQL commands.  
Users can add, view, update, and delete records while practicing database relationships and queries.

---

## 🧩 SPRINTS SUMMARY

### 🏗️ Sprint 1: Database Setup

```sql
CREATE DATABASE LibraryDB;
\c LibraryDB;

CREATE TABLE authors (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  nationality VARCHAR(50),
  birth_year INT,
  death_year INT
);

CREATE TABLE books (
  id SERIAL PRIMARY KEY,
  title VARCHAR(150) NOT NULL,
  author_id INT REFERENCES authors(id) ON DELETE CASCADE,
  genres TEXT[],
  published_year INT,
  available BOOLEAN DEFAULT TRUE
);

CREATE TABLE patrons (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  borrowed_books INT[]
);
```

### Sprint 2: Insert Sample Data
```sql
-- Authors
INSERT INTO authors (id, name, nationality, birth_year, death_year) VALUES
(1, 'George Orwell', 'British', 1903, 1950),
(2, 'Harper Lee', 'American', 1926, 2016),
(3, 'F. Scott Fitzgerald', 'American', 1896, 1940),
(4, 'Aldous Huxley', 'British', 1894, 1963),
(5, 'J.D. Salinger', 'American', 1919, 2010),
(6, 'Herman Melville', 'American', 1819, 1891),
(7, 'Jane Austen', 'British', 1775, 1817),
(8, 'Leo Tolstoy', 'Russian', 1828, 1910),
(9, 'Fyodor Dostoevsky', 'Russian', 1821, 1881),
(10, 'J.R.R. Tolkien', 'British', 1892, 1973);

-- Books
INSERT INTO books (id, title, author_id, genres, published_year, available) VALUES
(1, '1984', 1, ARRAY['Dystopian', 'Political Fiction'], 1949, TRUE),
(2, 'To Kill a Mockingbird', 2, ARRAY['Southern Gothic', 'Bildungsroman'], 1960, TRUE),
(3, 'The Great Gatsby', 3, ARRAY['Tragedy'], 1925, TRUE),
(4, 'Brave New World', 4, ARRAY['Dystopian', 'Science Fiction'], 1932, TRUE),
(5, 'The Catcher in the Rye', 5, ARRAY['Realist Novel', 'Bildungsroman'], 1951, TRUE),
(6, 'Moby-Dick', 6, ARRAY['Adventure Fiction'], 1851, TRUE),
(7, 'Pride and Prejudice', 7, ARRAY['Romantic Novel'], 1813, TRUE),
(8, 'War and Peace', 8, ARRAY['Historical Novel'], 1869, TRUE),
(9, 'Crime and Punishment', 9, ARRAY['Philosophical Novel'], 1866, TRUE),
(10, 'The Hobbit', 10, ARRAY['Fantasy'], 1937, TRUE);


-- Patrons
INSERT INTO patrons (id, name, email, borrowed_books) VALUES
(1, 'Alice Johnson', 'alice@example.com', ARRAY[]::INT[]),
(2, 'Bob Smith', 'bob@example.com', ARRAY[1, 2]),
(3, 'Carol White', 'carol@example.com', ARRAY[]::INT[]),
(4, 'David Brown', 'david@example.com', ARRAY[3]),
(5, 'Eve Davis', 'eve@example.com', ARRAY[]::INT[]),
(6, 'Frank Moore', 'frank@example.com', ARRAY[4, 5]),
(7, 'Grace Miller', 'grace@example.com', ARRAY[]::INT[]),
(8, 'Hank Wilson', 'hank@example.com', ARRAY[6]),
(9, 'Ivy Taylor', 'ivy@example.com', ARRAY[]::INT[]),
(10, 'Jack Anderson', 'jack@example.com', ARRAY[7, 8]);
```

### Sprint 3: Read Operations
-- Get all books
``` sql
SELECT * FROM books;
```
--

-- Get book by title
``` sql
SELECT * FROM books WHERE LOWER(title) = LOWER('1984');
```

-- Get books by author
```sql
SELECT b.title, a.name AS author
FROM books b
JOIN authors a ON b.author_id = a.id
WHERE LOWER(a.name) = LOWER('George Orwell');
```
-- Get all available books
```sql
SELECT * FROM books WHERE available = TRUE;
```

✏️ Sprint 4: Update Operations
```sql
-- Mark book as borrowed
UPDATE books SET available = FALSE WHERE title = '1984';
```
-- Add new genre
``` sql
UPDATE books SET genres = genres || 'Classic' WHERE title = '1984';
```
-- Add borrowed book to patron
``` sql
UPDATE patrons SET borrowed_books = borrowed_books || 1 WHERE name = 'Alice Johnson';
```
❌ Sprint 5: Delete Operations
-- Delete a book by title
```sql
DELETE FROM books WHERE LOWER(title) = LOWER('1984');
```

-- Delete an author by ID (deletes their books too)
```sql
DELETE FROM authors WHERE id = 1;
```
🧮 Sprint 6: Advanced Queries
-- Books published after 1950
```sql
SELECT * FROM books WHERE published_year > 1950;
```

-- All American authors
```sql
SELECT * FROM authors WHERE nationality = 'American';
```

-- Set all books available
```sql
UPDATE books SET available = TRUE;
```
-- Available books after 1950
```sql
SELECT * FROM books WHERE available = TRUE AND published_year > 1950;
```
-- Authors whose names contain "George"
```sql
SELECT * FROM authors WHERE name ILIKE '%George%';
```
-- Increment published year 1869 by 1
```sql
UPDATE books SET published_year = published_year + 1 WHERE published_year = 1869;
```
## Running the Project
### Option 1: Using pgAdmin

1. Open pgAdmin and connect to your PostgreSQL server.

2. Right-click on Databases → Create → Database, name it LibraryDB.

3. Open the Query Tool.

4. Copy and paste the SQL commands (from Sprints 1–6) in order.

5. Click Execute ▶️ to run.

6. Use SELECT queries to test your data.

### Option 2: Using psql (Terminal)
```bash
psql -U postgres
CREATE DATABASE LibraryDB;
\c LibraryDB
-- Paste your SQL commands here
```

To verify:
```sql
\dt  -- lists all tables
SELECT * FROM books;
```
## Project Complete

### Features Implemented:

* Database creation & setup

* Data insertion (authors, books, patrons)

* Read, Update, Delete, and Advanced queries

* Fully documented SQL workflow

## Author

- Your Name: Bongeka Bhungane
- Date: September 2025 
