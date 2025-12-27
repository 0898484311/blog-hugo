---
title: "Node.js cơ bản - JavaScript trên Server"
date: 2025-12-13
draft: false
description: "Tìm hiểu về Node.js - cách chạy JavaScript trên server side"
tags: ["JavaScript", "Node.js", "Backend", "Server", "NPM", "Express"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/nodejs.jpg"
  alt: "Node.js cơ bản"
  caption: "Node.js cơ bản"
---

## Giới thiệu

Node.js là một JavaScript runtime được xây dựng trên Chrome's V8 JavaScript engine. Nó cho phép chạy JavaScript trên server side, mở ra khả năng phát triển full-stack với một ngôn ngữ duy nhất.

## Node.js là gì?

**Node.js** là một platform cho phép chạy JavaScript bên ngoài browser. Nó sử dụng event-driven, non-blocking I/O model, làm cho nó nhẹ và hiệu quả cho các ứng dụng real-time.

### Đặc điểm chính

- ⚡ **Non-blocking I/O**: Xử lý nhiều request đồng thời
- 🚀 **Fast**: Được xây dựng trên V8 engine
- 📦 **NPM**: Package manager lớn nhất thế giới
- 🔄 **Event-driven**: Phù hợp cho real-time applications

## Cài đặt Node.js

### Kiểm tra phiên bản

```bash
node --version
npm --version
```

### Tạo project mới

```bash
mkdir my-node-app
cd my-node-app
npm init -y
```

## File System Module

### Đọc file

```javascript
const fs = require('fs');

// Đọc file đồng bộ
const data = fs.readFileSync('file.txt', 'utf8');
console.log(data);

// Đọc file bất đồng bộ
fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data);
});

// Với Promises (Node.js 10+)
const fsPromises = require('fs').promises;
async function readFile() {
    try {
        const data = await fsPromises.readFile('file.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
```

### Ghi file

```javascript
const fs = require('fs');

// Ghi file đồng bộ
fs.writeFileSync('output.txt', 'Hello Node.js');

// Ghi file bất đồng bộ
fs.writeFile('output.txt', 'Hello Node.js', (err) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log('File written successfully');
});
```

## HTTP Module

### Tạo HTTP Server

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end('<h1>Hello Node.js!</h1>');
});

server.listen(3000, () => {
    console.log('Server running on http://localhost:3000');
});
```

### Routing đơn giản

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    const url = req.url;
    
    if (url === '/') {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end('<h1>Home Page</h1>');
    } else if (url === '/about') {
        res.writeHead(200, { 'Content-Type': 'text/html' });
        res.end('<h1>About Page</h1>');
    } else {
        res.writeHead(404, { 'Content-Type': 'text/html' });
        res.end('<h1>404 Not Found</h1>');
    }
});

server.listen(3000);
```

## NPM - Node Package Manager

### Cài đặt package

```bash
# Local install
npm install express

# Global install
npm install -g nodemon

# Dev dependencies
npm install --save-dev jest
```

### package.json

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My Node.js app",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0"
  }
}
```

## Express.js Framework

### Cài đặt Express

```bash
npm install express
```

### Server đơn giản với Express

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
    res.send('Hello Express!');
});

app.get('/api/users', (req, res) => {
    res.json({ users: ['John', 'Jane'] });
});

app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
```

### Middleware

```javascript
const express = require('express');
const app = express();

// Built-in middleware
app.use(express.json()); // Parse JSON
app.use(express.urlencoded({ extended: true })); // Parse form data

// Custom middleware
app.use((req, res, next) => {
    console.log(`${req.method} ${req.path}`);
    next();
});

// Route-specific middleware
function authMiddleware(req, res, next) {
    const token = req.headers.authorization;
    if (token) {
        next();
    } else {
        res.status(401).json({ error: 'Unauthorized' });
    }
}

app.get('/protected', authMiddleware, (req, res) => {
    res.json({ message: 'Protected route' });
});
```

## Environment Variables

### Sử dụng dotenv

```bash
npm install dotenv
```

```javascript
require('dotenv').config();

const PORT = process.env.PORT || 3000;
const DB_URL = process.env.DATABASE_URL;

console.log(`Server running on port ${PORT}`);
```

### .env file

```
PORT=3000
DATABASE_URL=mongodb://localhost:27017/mydb
SECRET_KEY=your-secret-key
```

## Modules và Exports

### Export module

```javascript
// math.js
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

// Named exports
module.exports = { add, subtract };

// Hoặc
exports.add = add;
exports.subtract = subtract;
```

### Import module

```javascript
// app.js
const { add, subtract } = require('./math');

console.log(add(2, 3)); // 5
console.log(subtract(5, 2)); // 3
```

### ES6 Modules

```javascript
// math.mjs
export function add(a, b) {
    return a + b;
}

// app.mjs
import { add } from './math.mjs';
console.log(add(2, 3));
```

## Error Handling

```javascript
// Try-catch
async function fetchData() {
    try {
        const data = await getData();
        return data;
    } catch (error) {
        console.error('Error:', error.message);
        throw error;
    }
}

// Error middleware trong Express
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).json({ error: 'Something went wrong!' });
});
```

## Best Practices

✅ **Sử dụng async/await:**

```javascript
// Đúng
async function getData() {
    const data = await fetchData();
    return data;
}
```

✅ **Environment variables cho config:**

```javascript
const config = {
    port: process.env.PORT || 3000,
    dbUrl: process.env.DATABASE_URL
};
```

✅ **Error handling:**

```javascript
process.on('uncaughtException', (err) => {
    console.error('Uncaught Exception:', err);
    process.exit(1);
});
```

✅ **Logging:**

```javascript
const winston = require('winston');
const logger = winston.createLogger({
    level: 'info',
    format: winston.format.json(),
    transports: [
        new winston.transports.File({ filename: 'error.log', level: 'error' }),
        new winston.transports.File({ filename: 'combined.log' })
    ]
});
```

## Ứng dụng thực tế

Node.js được sử dụng trong:

- 🌐 **Web Servers**: Express, Koa, Fastify
- 📱 **APIs**: REST APIs, GraphQL
- 💬 **Real-time Apps**: Chat apps, Collaboration tools
- 🔄 **Microservices**: Service-oriented architecture
- 🛠️ **Build Tools**: Webpack, Gulp, Grunt
- 📊 **Data Processing**: ETL pipelines, Data streaming

## Kết luận

Node.js đã cách mạng hóa backend development bằng cách cho phép sử dụng JavaScript ở cả frontend và backend. Nó là công cụ mạnh mẽ cho việc xây dựng scalable, real-time applications.

## Tài liệu tham khảo

- [Node.js Official Documentation](https://nodejs.org/docs/)
- [Express.js Guide](https://expressjs.com/)
- [NPM Documentation](https://docs.npmjs.com/)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

---

**Bạn có câu hỏi về Node.js? Hãy để lại comment bên dưới!** 💬

