---
title: "ES6+ trong JavaScript - Tính năng mới quan trọng"
date: 2025-12-13
draft: false
description: "Tìm hiểu về ES6+ trong JavaScript - các tính năng mới từ ES2015 đến hiện tại"
tags: ["JavaScript", "ES6", "ES2015", "Modern JavaScript", "Arrow Functions", "Destructuring"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/es6.jpg"
  alt: "ES6+ trong JavaScript"
  caption: "ES6+ trong JavaScript"
---

## Giới thiệu

ES6 (ECMAScript 2015) là một bước ngoặt lớn trong lịch sử JavaScript, mang đến nhiều tính năng mới giúp code ngắn gọn, dễ đọc và mạnh mẽ hơn. Các phiên bản ES7, ES8, ES9... tiếp tục bổ sung thêm nhiều tính năng hữu ích.

## Let và Const

### Let - Block scoped variable

```javascript
// Var - function scoped
function example1() {
    if (true) {
        var x = 1;
    }
    console.log(x); // 1 - vẫn truy cập được
}

// Let - block scoped
function example2() {
    if (true) {
        let y = 1;
    }
    console.log(y); // ReferenceError
}
```

### Const - Constant variable

```javascript
const PI = 3.14159;
// PI = 3.14; // Error: Assignment to constant variable

const person = { name: "John" };
person.name = "Jane"; // OK - chỉ không thể reassign object
// person = {}; // Error
```

## Arrow Functions

### Cú pháp ngắn gọn

```javascript
// Function thông thường
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => {
    return a + b;
};

// Arrow function ngắn gọn
const add = (a, b) => a + b;

// Một tham số
const square = x => x * x;

// Không tham số
const greet = () => console.log("Hello");
```

### This binding

```javascript
// Function thông thường - this thay đổi
const obj = {
    name: "John",
    greet: function() {
        setTimeout(function() {
            console.log(this.name); // undefined
        }, 1000);
    }
};

// Arrow function - this giữ nguyên
const obj2 = {
    name: "John",
    greet: function() {
        setTimeout(() => {
            console.log(this.name); // "John"
        }, 1000);
    }
};
```

## Template Literals

```javascript
const name = "John";
const age = 30;

// Cách cũ
const message = "Tôi là " + name + ", " + age + " tuổi";

// Template literal
const message = `Tôi là ${name}, ${age} tuổi`;

// Multi-line strings
const html = `
    <div>
        <h1>${name}</h1>
        <p>Age: ${age}</p>
    </div>
`;
```

## Destructuring

### Array Destructuring

```javascript
const numbers = [1, 2, 3, 4, 5];

// Cách cũ
const first = numbers[0];
const second = numbers[1];

// Destructuring
const [first, second, ...rest] = numbers;
console.log(first); // 1
console.log(rest);  // [3, 4, 5]

// Skip elements
const [, , third] = numbers;
console.log(third); // 3
```

### Object Destructuring

```javascript
const person = {
    name: "John",
    age: 30,
    city: "Hanoi"
};

// Cách cũ
const name = person.name;
const age = person.age;

// Destructuring
const { name, age } = person;

// Rename
const { name: fullName, age: years } = person;

// Default values
const { name, age, country = "Vietnam" } = person;
```

## Spread Operator

### Array Spread

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// Combine arrays
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Copy array
const copy = [...arr1];

// Add elements
const newArr = [0, ...arr1, 4]; // [0, 1, 2, 3, 4]
```

### Object Spread

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };

// Merge objects
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3, d: 4 }

// Override properties
const updated = { ...obj1, b: 5 }; // { a: 1, b: 5 }
```

## Default Parameters

```javascript
// Cách cũ
function greet(name) {
    name = name || "Guest";
    console.log(`Hello, ${name}`);
}

// ES6
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet();        // "Hello, Guest"
greet("John");  // "Hello, John"
```

## Rest Parameters

```javascript
// Cách cũ
function sum() {
    let total = 0;
    for (let i = 0; i < arguments.length; i++) {
        total += arguments[i];
    }
    return total;
}

// ES6
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

sum(1, 2, 3, 4); // 10
```

## Classes

```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    static createBaby(name) {
        return new Person(name, 0);
    }
}

class Student extends Person {
    constructor(name, age, school) {
        super(name, age);
        this.school = school;
    }
    
    study() {
        return `${this.name} is studying at ${this.school}`;
    }
}

const student = new Student("John", 20, "University");
console.log(student.greet()); // "Hello, I'm John"
```

## Modules (ES6)

### Export

```javascript
// math.js
export const PI = 3.14159;

export function add(a, b) {
    return a + b;
}

export default function multiply(a, b) {
    return a * b;
}
```

### Import

```javascript
// app.js
import multiply, { PI, add } from './math.js';

console.log(add(2, 3)); // 5
console.log(multiply(2, 3)); // 6
```

## Promises và Async/Await

### Promises

```javascript
const fetchData = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Data received");
        }, 1000);
    });
};

fetchData()
    .then(data => console.log(data))
    .catch(error => console.error(error));
```

### Async/Await (ES2017)

```javascript
async function getData() {
    try {
        const data = await fetchData();
        console.log(data);
    } catch (error) {
        console.error(error);
    }
}
```

## Array Methods mới

```javascript
const numbers = [1, 2, 3, 4, 5];

// find
const found = numbers.find(n => n > 3); // 4

// findIndex
const index = numbers.findIndex(n => n > 3); // 3

// includes
const hasThree = numbers.includes(3); // true

// map
const doubled = numbers.map(n => n * 2); // [2, 4, 6, 8, 10]

// filter
const evens = numbers.filter(n => n % 2 === 0); // [2, 4]

// reduce
const sum = numbers.reduce((acc, n) => acc + n, 0); // 15
```

## Ứng dụng thực tế

ES6+ được sử dụng trong:

- 🌐 **Modern Web Development**: React, Vue, Angular
- 📱 **Mobile Apps**: React Native
- 🖥️ **Desktop Apps**: Electron
- ⚙️ **Backend**: Node.js
- 🔧 **Build Tools**: Webpack, Babel

## Kết luận

ES6+ đã thay đổi cách chúng ta viết JavaScript. Các tính năng mới giúp code ngắn gọn, dễ đọc và mạnh mẽ hơn. Nắm vững ES6+ là điều cần thiết cho mọi JavaScript developer.

## Tài liệu tham khảo

- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [ES6 Features](https://github.com/lukehoban/es6features)
- [JavaScript.info](https://javascript.info/)

---

**Bạn có câu hỏi về ES6+? Hãy để lại comment bên dưới!** 💬

