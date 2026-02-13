cat > README.md << 'EOF'
# Blog API with MongoDB

A RESTful Blog API built with Express.js and MongoDB, featuring user authentication, authorization, and full CRUD operations for blog posts.

## Features

- **User Authentication** - Register and login with JWT tokens
- **User Authorization** - Users can only modify/delete their own posts
- **CRUD Operations** - Create, read, update, delete blog posts
- **Data Validation** - Email and password validation
- **Password Security** - bcryptjs for password hashing
- **MongoDB** - Mongoose for database operations

## Tech Stack

- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM (Object Document Mapper)
- **bcryptjs** - Password hashing
- **jsonwebtoken** - JWT authentication

## Installation
```bash
npm install
```

## Running

Make sure MongoDB is running:
```bash
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

Then start the server:
```bash
node app.js
```

Server runs on: `http://localhost:3000`

## API Endpoints

### Users

- `POST /users` - Register new user
```
  Body: { email, password, name }
```

- `POST /login` - Login and get JWT token
```
  Body: { email, password }
  Returns: { token, user }
```

### Posts

- `GET /posts` - Get all posts

- `POST /posts` - Create new post (requires authentication)
```
  Headers: Authorization: Bearer <token>
  Body: { title, content }
```

- `GET /posts/:id` - Get specific post

- `PUT /posts/:id` - Update own post (requires authentication)
```
  Headers: Authorization: Bearer <token>
  Body: { title, content }
```

- `DELETE /posts/:id` - Delete own post (requires authentication)
```
  Headers: Authorization: Bearer <token>
```

## Example Usage

### Register User
```bash
curl -X POST http://localhost:3000/users \
  -H "Content-Type: application/json" \
  -d '{"email":"john@test.com","password":"john123","name":"John"}'
```

### Login
```bash
curl -X POST http://localhost:3000/login \
  -H "Content-Type: application/json" \
  -d '{"email":"john@test.com","password":"john123"}'
```

### Create Post
```bash
curl -X POST http://localhost:3000/posts \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{"title":"My Post","content":"This is my post"}'
```

## Project Structure
```
├── app.js           - Application entry point
├── package.json     - Dependencies
├── README.md        - This file
└── node_modules/    - Dependencies (not in git)
```

## Security Features

- ✅ Passwords are hashed with bcryptjs (10 rounds)
- ✅ JWT tokens for authentication
- ✅ Authorization checks - users can only modify their own posts
- ✅ Email validation on registration
- ✅ Password validation on login

## Learning Outcomes

This project demonstrates:
- Express.js REST API development
- MongoDB and Mongoose for data persistence
- JWT authentication flow
- Password hashing and security
- Authorization and access control
- Error handling and validation
EOF