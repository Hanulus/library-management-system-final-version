# Library Management REST API - Spring Boot

Simple REST API using Spring Boot.

## Project Structure

```
src/
├── main/
│   ├── java/
│   │   ├── LibraryApplication.java      # Main Spring Boot app
│   │   ├── BookController.java          # REST endpoints for books
│   │   ├── MemberController.java        # REST endpoints for members
│   │   ├── BookDAO.java                 # Database operations for books
│   │   ├── MemberDAO.java               # Database operations for members
│   │   ├── DatabaseManager.java         # Database connection
│   │   ├── Book.java, EBook.java, PhysicalBook.java
│   │   └── LibraryMember.java
│   └── resources/
│       └── application.properties       # Spring Boot config
└── sql/
    └── schema.sql
```

## Setup

1. Create database:
```sql
CREATE DATABASE library_db;
```

2. Run schema.sql

3. Update DatabaseManager.java with your password

4. Run:
```bash
mvn spring-boot:run
```

Server starts on: http://localhost:8080

## API Endpoints

### Books

**GET /api/books** - Get all books
```bash
curl http://localhost:8080/api/books
```

**GET /api/books/{isbn}** - Get book by ISBN
```bash
curl http://localhost:8080/api/books/ISBN-001
```

**POST /api/books** - Create new book
```bash
# Physical Book
curl -X POST http://localhost:8080/api/books \
  -H "Content-Type: application/json" \
  -d '{
    "title": "New Book",
    "author": "Author Name",
    "isbn": "ISBN-999",
    "bookType": "PhysicalBook",
    "shelfNumber": 10
  }'

# EBook
curl -X POST http://localhost:8080/api/books \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Digital Book",
    "author": "Author Name",
    "isbn": "ISBN-888",
    "bookType": "EBook",
    "fileSizeMB": 3.5
  }'
```

**PUT /api/books/{isbn}** - Update availability
```bash
curl -X PUT http://localhost:8080/api/books/ISBN-001 \
  -H "Content-Type: application/json" \
  -d '{"isAvailable": false}'
```

**DELETE /api/books/{isbn}** - Delete book
```bash
curl -X DELETE http://localhost:8080/api/books/ISBN-001
```

### Members

**GET /api/members** - Get all members
```bash
curl http://localhost:8080/api/members
```

**GET /api/members/{memberId}** - Get member by ID
```bash
curl http://localhost:8080/api/members/M001
```

**POST /api/members** - Create new member
```bash
curl -X POST http://localhost:8080/api/members \
  -H "Content-Type: application/json" \
  -d '{
    "name": "New Member",
    "memberId": "M999",
    "email": "member@email.com"
  }'
```

**DELETE /api/members/{memberId}** - Delete member
```bash
curl -X DELETE http://localhost:8080/api/members/M001
```

## How It Works

1. **@RestController** - marks class as REST API controller
2. **@RequestMapping** - sets base URL path
3. **@GetMapping** - handles GET requests
4. **@PostMapping** - handles POST requests (create)
5. **@PutMapping** - handles PUT requests (update)
6. **@DeleteMapping** - handles DELETE requests
7. **@PathVariable** - extracts value from URL
8. **@RequestBody** - converts JSON to Java object

Spring Boot automatically converts Java objects to JSON.
