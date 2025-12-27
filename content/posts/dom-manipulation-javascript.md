---
title: "DOM Manipulation trong JavaScript - Thao tác với HTML"
date: 2025-12-13
draft: false
description: "Tìm hiểu về DOM Manipulation trong JavaScript - cách thao tác với HTML elements"
tags: ["JavaScript", "DOM", "HTML", "Web Development", "Frontend"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/dom.jpg"
  alt: "DOM Manipulation trong JavaScript"
  caption: "DOM Manipulation trong JavaScript"
---

## Giới thiệu

DOM (Document Object Model) là biểu diễn của HTML document dưới dạng cây đối tượng. JavaScript cho phép chúng ta thao tác với DOM để thay đổi nội dung, style và cấu trúc của trang web một cách động.

## DOM là gì?

**DOM** là một programming interface cho HTML và XML documents. Nó biểu diễn document như một cây các nodes, mỗi node đại diện cho một phần của document.

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <h1>Hello World</h1>
    <p id="demo">This is a paragraph</p>
</body>
</html>
```

## Truy cập Elements

### getElementById

```javascript
const element = document.getElementById("demo");
console.log(element.textContent); // "This is a paragraph"
```

### getElementsByClassName

```javascript
const elements = document.getElementsByClassName("my-class");
// Trả về HTMLCollection
for (let i = 0; i < elements.length; i++) {
    console.log(elements[i]);
}
```

### getElementsByTagName

```javascript
const paragraphs = document.getElementsByTagName("p");
// Trả về tất cả thẻ <p>
```

### querySelector và querySelectorAll

```javascript
// querySelector - trả về element đầu tiên
const element = document.querySelector("#demo");
const firstP = document.querySelector("p");

// querySelectorAll - trả về NodeList
const allP = document.querySelectorAll("p");
allP.forEach(p => console.log(p));
```

## Thay đổi Nội dung

### textContent và innerHTML

```javascript
const element = document.getElementById("demo");

// textContent - chỉ text, an toàn hơn
element.textContent = "New text content";

// innerHTML - có thể chứa HTML tags
element.innerHTML = "<strong>Bold text</strong>";
```

### innerText

```javascript
element.innerText = "Visible text only";
// Chỉ lấy text hiển thị, bỏ qua hidden elements
```

## Thay đổi Attributes

### getAttribute và setAttribute

```javascript
const link = document.querySelector("a");

// Lấy attribute
const href = link.getAttribute("href");

// Set attribute
link.setAttribute("href", "https://example.com");
link.setAttribute("target", "_blank");

// Remove attribute
link.removeAttribute("target");
```

### ClassList

```javascript
const element = document.getElementById("myDiv");

// Thêm class
element.classList.add("active");
element.classList.add("highlight");

// Xóa class
element.classList.remove("active");

// Toggle class
element.classList.toggle("active");

// Kiểm tra class
if (element.classList.contains("active")) {
    console.log("Element is active");
}
```

## Thay đổi Style

### style property

```javascript
const element = document.getElementById("myDiv");

// Thay đổi style trực tiếp
element.style.color = "red";
element.style.backgroundColor = "blue";
element.style.fontSize = "20px";

// CSS properties với dấu gạch ngang → camelCase
element.style.marginTop = "10px";
element.style.borderRadius = "5px";
```

### className

```javascript
// Thay đổi toàn bộ class
element.className = "new-class another-class";

// Thêm class (giữ nguyên class cũ)
element.className += " additional-class";
```

## Tạo và Xóa Elements

### createElement

```javascript
// Tạo element mới
const newDiv = document.createElement("div");
newDiv.textContent = "New div element";
newDiv.className = "my-div";

// Thêm vào DOM
document.body.appendChild(newDiv);
```

### appendChild và insertBefore

```javascript
const parent = document.getElementById("parent");
const newElement = document.createElement("p");
newElement.textContent = "New paragraph";

// Thêm vào cuối
parent.appendChild(newElement);

// Thêm vào trước element khác
const existingElement = document.getElementById("existing");
parent.insertBefore(newElement, existingElement);
```

### removeChild và remove

```javascript
const parent = document.getElementById("parent");
const child = document.getElementById("child");

// Cách 1: removeChild
parent.removeChild(child);

// Cách 2: remove (ES6)
child.remove();
```

## Event Handling

### addEventListener

```javascript
const button = document.getElementById("myButton");

button.addEventListener("click", function() {
    console.log("Button clicked!");
});

// Arrow function
button.addEventListener("click", () => {
    console.log("Button clicked!");
});

// Named function
function handleClick() {
    console.log("Button clicked!");
}
button.addEventListener("click", handleClick);
```

### Event Object

```javascript
button.addEventListener("click", function(event) {
    console.log(event.type);        // "click"
    console.log(event.target);      // Element được click
    console.log(event.clientX);     // Tọa độ X
    console.log(event.clientY);     // Tọa độ Y
    
    // Ngăn default behavior
    event.preventDefault();
    
    // Ngăn event bubbling
    event.stopPropagation();
});
```

### Common Events

```javascript
// Click
element.addEventListener("click", handler);

// Mouse events
element.addEventListener("mouseenter", handler);
element.addEventListener("mouseleave", handler);
element.addEventListener("mousemove", handler);

// Keyboard events
element.addEventListener("keydown", handler);
element.addEventListener("keyup", handler);

// Form events
form.addEventListener("submit", handler);
input.addEventListener("change", handler);
input.addEventListener("input", handler);

// Window events
window.addEventListener("load", handler);
window.addEventListener("resize", handler);
window.addEventListener("scroll", handler);
```

## Traversing DOM

### Parent và Children

```javascript
const element = document.getElementById("child");

// Parent
const parent = element.parentElement;

// Children
const children = element.children; // HTMLCollection
const firstChild = element.firstElementChild;
const lastChild = element.lastElementChild;

// Siblings
const nextSibling = element.nextElementSibling;
const previousSibling = element.previousElementSibling;
```

### querySelector trong element

```javascript
const container = document.getElementById("container");

// Tìm trong container
const child = container.querySelector(".child");
const allChildren = container.querySelectorAll(".child");
```

## Best Practices

✅ **Sử dụng querySelector thay vì getElementById khi có thể:**

```javascript
// Modern và linh hoạt hơn
const element = document.querySelector("#myId");
```

✅ **Cache DOM elements:**

```javascript
// Sai - query nhiều lần
for (let i = 0; i < 100; i++) {
    document.getElementById("myDiv").style.color = "red";
}

// Đúng - cache element
const myDiv = document.getElementById("myDiv");
for (let i = 0; i < 100; i++) {
    myDiv.style.color = "red";
}
```

✅ **Sử dụng textContent thay vì innerHTML khi chỉ cần text:**

```javascript
// An toàn hơn, tránh XSS
element.textContent = userInput;

// Chỉ dùng innerHTML khi cần HTML
element.innerHTML = "<strong>Bold</strong>";
```

✅ **Event Delegation:**

```javascript
// Thay vì thêm listener cho từng button
const container = document.getElementById("container");
container.addEventListener("click", function(event) {
    if (event.target.classList.contains("button")) {
        // Xử lý click
    }
});
```

## Ứng dụng thực tế

DOM Manipulation được sử dụng trong:

- 🌐 **Interactive Websites**: Form validation, dynamic content
- 📱 **Single Page Applications**: React, Vue, Angular
- 🎮 **Web Games**: Game UI và interactions
- 📊 **Data Visualization**: Charts và graphs
- 🛒 **E-commerce**: Shopping carts, product filters

## Kết luận

DOM Manipulation là kỹ năng cơ bản nhưng quan trọng trong JavaScript. Nắm vững các phương thức và best practices sẽ giúp bạn xây dựng các ứng dụng web tương tác hiệu quả.

## Tài liệu tham khảo

- [MDN DOM Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)
- [JavaScript.info DOM](https://javascript.info/dom-nodes)
- [W3Schools DOM Tutorial](https://www.w3schools.com/js/js_htmldom.asp)

---

**Bạn có câu hỏi về DOM Manipulation? Hãy để lại comment bên dưới!** 💬

