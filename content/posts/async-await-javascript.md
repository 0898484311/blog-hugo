---
title: "Async/Await trong JavaScript - Xử lý bất đồng bộ"
date: 2025-12-13
draft: false
description: "Tìm hiểu về Async/Await trong JavaScript - cách xử lý bất đồng bộ một cách dễ đọc"
tags: ["JavaScript", "Async", "Await", "Promises", "Asynchronous", "ES2017"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/async.jpg"
  alt: "Async/Await trong JavaScript"
  caption: "Async/Await trong JavaScript"
---

## Giới thiệu

Async/Await là cú pháp được giới thiệu trong ES2017, giúp viết code bất đồng bộ dễ đọc và dễ hiểu hơn so với Promises. Nó cho phép viết code bất đồng bộ theo cách đồng bộ.

## Vấn đề với Callbacks

### Callback Hell

```javascript
// Callback hell - khó đọc và maintain
getData(function(data) {
    processData(data, function(result) {
        saveData(result, function(saved) {
            displayData(saved, function() {
                console.log("Done!");
            });
        });
    });
});
```

## Promises - Giải pháp đầu tiên

### Promise cơ bản

```javascript
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = "Data from server";
            resolve(data);
            // hoặc reject(new Error("Error message"));
        }, 1000);
    });
}

fetchData()
    .then(data => {
        console.log(data);
        return processData(data);
    })
    .then(result => {
        console.log(result);
    })
    .catch(error => {
        console.error(error);
    });
```

## Async/Await - Giải pháp hiện đại

### Cú pháp cơ bản

```javascript
// Function phải có async
async function fetchData() {
    // await chỉ hoạt động trong async function
    const data = await fetchDataFromServer();
    console.log(data);
    return data;
}
```

### So sánh Promise và Async/Await

```javascript
// Với Promise
function getUserData(userId) {
    return fetch(`/api/users/${userId}`)
        .then(response => response.json())
        .then(user => {
            return fetch(`/api/posts/${user.id}`);
        })
        .then(response => response.json())
        .catch(error => {
            console.error(error);
        });
}

// Với Async/Await
async function getUserData(userId) {
    try {
        const userResponse = await fetch(`/api/users/${userId}`);
        const user = await userResponse.json();
        
        const postsResponse = await fetch(`/api/posts/${user.id}`);
        const posts = await postsResponse.json();
        
        return posts;
    } catch (error) {
        console.error(error);
    }
}
```

## Xử lý Lỗi với Try-Catch

```javascript
async function fetchData() {
    try {
        const response = await fetch('/api/data');
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        return data;
    } catch (error) {
        console.error("Error fetching data:", error);
        // Có thể throw lại hoặc return default value
        throw error;
    }
}
```

## Multiple Async Operations

### Sequential (Tuần tự)

```javascript
async function fetchSequential() {
    const user = await fetchUser();
    const posts = await fetchPosts(user.id);
    const comments = await fetchComments(posts[0].id);
    
    return { user, posts, comments };
}
```

### Parallel (Song song)

```javascript
async function fetchParallel() {
    // Chạy đồng thời, nhanh hơn
    const [user, posts, comments] = await Promise.all([
        fetchUser(),
        fetchPosts(),
        fetchComments()
    ]);
    
    return { user, posts, comments };
}
```

### Promise.allSettled

```javascript
async function fetchAll() {
    const results = await Promise.allSettled([
        fetchUser(),
        fetchPosts(),
        fetchComments()
    ]);
    
    // Xử lý từng kết quả, không bị dừng nếu một promise fail
    results.forEach((result, index) => {
        if (result.status === 'fulfilled') {
            console.log(`Success ${index}:`, result.value);
        } else {
            console.error(`Error ${index}:`, result.reason);
        }
    });
}
```

## Async trong Loops

### For Loop

```javascript
async function processItems(items) {
    for (const item of items) {
        await processItem(item); // Chờ từng item
    }
}
```

### Map với Promise.all

```javascript
async function processItemsParallel(items) {
    const results = await Promise.all(
        items.map(item => processItem(item))
    );
    return results;
}
```

## Async Function trong Classes

```javascript
class ApiClient {
    async getUser(userId) {
        const response = await fetch(`/api/users/${userId}`);
        return response.json();
    }
    
    async createUser(userData) {
        const response = await fetch('/api/users', {
            method: 'POST',
            body: JSON.stringify(userData),
            headers: { 'Content-Type': 'application/json' }
        });
        return response.json();
    }
}

// Sử dụng
const client = new ApiClient();
const user = await client.getUser(1);
```

## Top-level Await (ES2022)

```javascript
// Có thể dùng await ở top-level trong modules
const data = await fetch('/api/data').then(r => r.json());
console.log(data);
```

## Best Practices

✅ **Luôn sử dụng try-catch:**

```javascript
async function safeFetch() {
    try {
        const data = await fetchData();
        return data;
    } catch (error) {
        // Xử lý lỗi
        console.error(error);
        return null;
    }
}
```

✅ **Sử dụng Promise.all cho operations độc lập:**

```javascript
// Nhanh hơn
const [user, posts] = await Promise.all([
    fetchUser(),
    fetchPosts()
]);
```

✅ **Không dùng await trong loops không cần thiết:**

```javascript
// Sai - chậm
for (const item of items) {
    await processItem(item);
}

// Đúng - nhanh hơn
await Promise.all(items.map(item => processItem(item)));
```

✅ **Return promises từ async functions:**

```javascript
// Đúng
async function getData() {
    return await fetch('/api/data');
}

// Cũng đúng - không cần await nếu chỉ return
async function getData() {
    return fetch('/api/data');
}
```

## Ứng dụng thực tế

Async/Await được sử dụng trong:

- 🌐 **API Calls**: Fetch data từ server
- 📱 **Mobile Apps**: React Native, Ionic
- 🖥️ **Desktop Apps**: Electron
- ⚙️ **Backend**: Node.js, Express
- 🔄 **Real-time Apps**: WebSockets, Server-Sent Events

## Kết luận

Async/Await làm cho code bất đồng bộ dễ đọc và dễ maintain hơn. Nó là công cụ quan trọng trong modern JavaScript development.

## Tài liệu tham khảo

- [MDN Async/Await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [JavaScript.info Async/Await](https://javascript.info/async-await)
- [Promise MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

---

**Bạn có câu hỏi về Async/Await? Hãy để lại comment bên dưới!** 💬

