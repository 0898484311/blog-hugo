---
title: "OOP trong Java - Lập trình hướng đối tượng"
date: 2025-12-13
draft: false
description: "Tìm hiểu về OOP trong Java - 4 nguyên lý cơ bản và cách áp dụng"
tags: ["Java", "OOP", "Object-Oriented", "Encapsulation", "Inheritance", "Polymorphism"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/oop.jpg"
  alt: "OOP trong Java"
  caption: "OOP trong Java"
---

## Giới thiệu

Lập trình hướng đối tượng (OOP) là paradigm chính trong Java. Nó giúp code dễ hiểu, dễ maintain và tái sử dụng. Java hỗ trợ đầy đủ 4 nguyên lý cơ bản của OOP.

## 4 Nguyên lý OOP

### 1. Encapsulation (Đóng gói)

Ẩn chi tiết implementation và chỉ expose những gì cần thiết:

```java
public class BankAccount {
    // Private fields - ẩn implementation
    private double balance;
    private String accountNumber;
    
    // Public methods - interface
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        }
    }
    
    public double getBalance() {
        return balance;
    }
}
```

**Lợi ích:**
- Bảo vệ dữ liệu khỏi truy cập trực tiếp
- Dễ thay đổi implementation
- Validation dữ liệu tập trung

### 2. Inheritance (Kế thừa)

Class con kế thừa properties và methods từ class cha:

```java
// Class cha
public class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public void eat() {
        System.out.println(name + " đang ăn");
    }
}

// Class con
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    public void bark() {
        System.out.println(name + " đang sủa");
    }
}

// Sử dụng
Dog dog = new Dog("Buddy");
dog.eat();  // Kế thừa từ Animal
dog.bark(); // Method riêng của Dog
```

### 3. Polymorphism (Đa hình)

Một interface có nhiều implementation:

```java
// Interface
interface Shape {
    double calculateArea();
}

// Implementation 1
class Circle implements Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

// Implementation 2
class Rectangle implements Shape {
    private double width, height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public double calculateArea() {
        return width * height;
    }
}

// Sử dụng đa hình
Shape[] shapes = {
    new Circle(5),
    new Rectangle(4, 6)
};

for (Shape shape : shapes) {
    System.out.println("Area: " + shape.calculateArea());
}
```

### 4. Abstraction (Trừu tượng)

Ẩn chi tiết phức tạp, chỉ hiển thị những gì cần thiết:

```java
// Abstract class
abstract class Vehicle {
    protected String brand;
    
    public Vehicle(String brand) {
        this.brand = brand;
    }
    
    // Abstract method - phải được implement
    public abstract void start();
    
    // Concrete method
    public void stop() {
        System.out.println(brand + " đã dừng");
    }
}

// Implementation
class Car extends Vehicle {
    public Car(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println(brand + " khởi động bằng chìa khóa");
    }
}

class ElectricCar extends Vehicle {
    public ElectricCar(String brand) {
        super(brand);
    }
    
    @Override
    public void start() {
        System.out.println(brand + " khởi động bằng nút bấm");
    }
}
```

## Access Modifiers

```java
public class Example {
    public int publicVar;      // Truy cập từ mọi nơi
    protected int protectedVar; // Truy cập trong package và subclass
    int defaultVar;             // Truy cập trong cùng package
    private int privateVar;     // Chỉ truy cập trong class
}
```

## Method Overloading

Cùng tên method nhưng khác parameters:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
    
    public int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

## Method Overriding

Ghi đè method từ class cha:

```java
class Parent {
    public void display() {
        System.out.println("Parent class");
    }
}

class Child extends Parent {
    @Override
    public void display() {
        System.out.println("Child class");
    }
}
```

## Interface

Định nghĩa contract mà class phải implement:

```java
interface Flyable {
    void fly();
}

interface Swimmable {
    void swim();
}

// Class có thể implement nhiều interface
class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck đang bay");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck đang bơi");
    }
}
```

## Best Practices

✅ **Sử dụng composition thay vì inheritance khi có thể:**

```java
// Composition
class Car {
    private Engine engine;
    
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

✅ **Favor interfaces over abstract classes:**

```java
// Interface - linh hoạt hơn
interface Drawable {
    void draw();
}
```

✅ **Single Responsibility Principle:**

```java
// Mỗi class chỉ có một trách nhiệm
class UserService {
    public void createUser() { }
    public void deleteUser() { }
}
```

✅ **Dependency Injection:**

```java
class UserController {
    private UserService userService;
    
    public UserController(UserService userService) {
        this.userService = userService;
    }
}
```

## Ứng dụng thực tế

OOP được sử dụng trong:

- 🏗️ **Software Architecture**: Thiết kế hệ thống lớn
- 📱 **Mobile Development**: Android, iOS apps
- 🌐 **Web Development**: Backend frameworks
- 🎮 **Game Development**: Game objects và logic
- 💼 **Enterprise Applications**: Business logic modeling

## Kết luận

OOP là nền tảng của lập trình Java. Hiểu rõ và áp dụng đúng 4 nguyên lý sẽ giúp bạn viết code chất lượng, dễ maintain và mở rộng.

## Tài liệu tham khảo

- [Oracle Java OOP Tutorial](https://docs.oracle.com/javase/tutorial/java/concepts/)
- Java API Documentation
- Design Patterns in Java

---

**Bạn có câu hỏi về OOP? Hãy để lại comment bên dưới!** 💬

