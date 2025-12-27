---
title: "Exception Handling trong Java - Xử lý lỗi đúng cách"
date: 2025-12-13
draft: false
description: "Tìm hiểu về Exception Handling trong Java - cách xử lý lỗi một cách chuyên nghiệp"
tags: ["Java", "Exception", "Error Handling", "Try-Catch", "Best Practices"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/exception.jpg"
  alt: "Exception Handling trong Java"
  caption: "Exception Handling trong Java"
---

## Giới thiệu

Exception Handling là một trong những khái niệm quan trọng nhất trong Java. Nó cho phép chương trình xử lý các tình huống bất thường một cách graceful, tránh crash và cung cấp thông tin hữu ích cho việc debug.

## Exception là gì?

**Exception** là một sự kiện bất thường xảy ra trong quá trình thực thi chương trình, làm gián đoạn luồng xử lý bình thường. Java có hệ thống exception handling mạnh mẽ để quản lý các lỗi này.

## Phân loại Exception

### 1. Checked Exception

Phải được xử lý hoặc khai báo trong method signature:

```java
// FileNotFoundException là checked exception
public void readFile() throws FileNotFoundException {
    FileReader file = new FileReader("file.txt");
}
```

**Ví dụ:**
- `IOException`
- `FileNotFoundException`
- `SQLException`
- `ClassNotFoundException`

### 2. Unchecked Exception (Runtime Exception)

Không bắt buộc phải xử lý:

```java
// NullPointerException là unchecked exception
String str = null;
int length = str.length(); // Ném NullPointerException
```

**Ví dụ:**
- `NullPointerException`
- `ArrayIndexOutOfBoundsException`
- `ArithmeticException`
- `IllegalArgumentException`

### 3. Error

Lỗi nghiêm trọng, thường không thể xử lý:

```java
// OutOfMemoryError
int[] hugeArray = new int[Integer.MAX_VALUE];
```

## Cấu trúc Try-Catch-Finally

### Cú pháp cơ bản

```java
try {
    // Code có thể ném exception
    int result = 10 / 0;
} catch (ArithmeticException e) {
    // Xử lý exception
    System.out.println("Lỗi chia cho 0: " + e.getMessage());
} finally {
    // Luôn được thực thi
    System.out.println("Finally block");
}
```

### Multiple Catch Blocks

```java
try {
    int[] arr = new int[5];
    arr[10] = 100; // ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Lỗi index: " + e.getMessage());
} catch (Exception e) {
    System.out.println("Lỗi khác: " + e.getMessage());
}
```

### Try-With-Resources

Tự động đóng resources:

```java
try (FileReader file = new FileReader("file.txt");
     BufferedReader reader = new BufferedReader(file)) {
    
    String line = reader.readLine();
    System.out.println(line);
    
} catch (IOException e) {
    System.out.println("Lỗi đọc file: " + e.getMessage());
}
// FileReader và BufferedReader tự động được đóng
```

## Tạo Custom Exception

### Tạo Checked Exception

```java
public class InsufficientFundsException extends Exception {
    private double amount;
    
    public InsufficientFundsException(double amount) {
        super("Số tiền không đủ: " + amount);
        this.amount = amount;
    }
    
    public double getAmount() {
        return amount;
    }
}
```

### Sử dụng Custom Exception

```java
public class BankAccount {
    private double balance;
    
    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException(amount);
        }
        balance -= amount;
    }
}
```

## Best Practices

✅ **Catch specific exceptions:**

```java
// Đúng
try {
    // code
} catch (FileNotFoundException e) {
    // xử lý cụ thể
}

// Sai - quá chung chung
try {
    // code
} catch (Exception e) {
    // xử lý tất cả
}
```

✅ **Không bỏ qua exception:**

```java
// Sai
try {
    riskyOperation();
} catch (Exception e) {
    // Bỏ qua - rất nguy hiểm!
}

// Đúng
try {
    riskyOperation();
} catch (Exception e) {
    logger.error("Lỗi xảy ra", e);
    // Hoặc throw lại
    throw new CustomException("Lỗi xử lý", e);
}
```

✅ **Sử dụng finally cho cleanup:**

```java
Connection conn = null;
try {
    conn = getConnection();
    // Sử dụng connection
} catch (SQLException e) {
    // Xử lý lỗi
} finally {
    if (conn != null) {
        try {
            conn.close();
        } catch (SQLException e) {
            logger.error("Lỗi đóng connection", e);
        }
    }
}
```

✅ **Throw early, catch late:**

```java
public void processUser(String username) {
    if (username == null || username.isEmpty()) {
        throw new IllegalArgumentException("Username không được null hoặc rỗng");
    }
    // Xử lý tiếp
}
```

## Exception Chaining

Giữ nguyên thông tin exception gốc:

```java
try {
    // code
} catch (IOException e) {
    throw new CustomException("Lỗi xử lý file", e);
}
```

## Common Exceptions

### NullPointerException

```java
String str = null;
// Sai
int length = str.length();

// Đúng
if (str != null) {
    int length = str.length();
}
```

### ArrayIndexOutOfBoundsException

```java
int[] arr = {1, 2, 3};
// Sai
int value = arr[10];

// Đúng
if (index >= 0 && index < arr.length) {
    int value = arr[index];
}
```

### NumberFormatException

```java
String number = "abc";
// Sai
int num = Integer.parseInt(number);

// Đúng
try {
    int num = Integer.parseInt(number);
} catch (NumberFormatException e) {
    System.out.println("Không thể chuyển đổi: " + number);
}
```

## Ứng dụng thực tế

Exception handling được sử dụng trong:

- 📁 **File Operations**: Xử lý lỗi đọc/ghi file
- 🌐 **Network Programming**: Xử lý lỗi kết nối mạng
- 💾 **Database Operations**: Xử lý lỗi SQL
- 🔐 **Authentication**: Xử lý lỗi đăng nhập
- 📊 **Data Validation**: Kiểm tra dữ liệu đầu vào

## Kết luận

Exception Handling là kỹ năng quan trọng trong Java. Xử lý exception đúng cách giúp code robust, dễ maintain và cung cấp trải nghiệm tốt cho người dùng.

## Tài liệu tham khảo

- [Oracle Java Exception Tutorial](https://docs.oracle.com/javase/tutorial/essential/exceptions/)
- Java API Documentation: `java.lang.Exception`
- Java API Documentation: `java.lang.RuntimeException`

---

**Bạn có câu hỏi về Exception Handling? Hãy để lại comment bên dưới!** 💬

