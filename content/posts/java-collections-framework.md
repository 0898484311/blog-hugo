---
title: "Java Collections Framework - Hướng dẫn toàn diện"
date: 2025-12-13
draft: false
description: "Tìm hiểu về Java Collections Framework - các cấu trúc dữ liệu quan trọng trong Java"
tags: ["Java", "Collections", "Data Structures", "ArrayList", "HashMap"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/collections.jpg"
  alt: "Java Collections Framework"
  caption: "Java Collections Framework"
---

## Giới thiệu

Java Collections Framework là một trong những phần quan trọng nhất của Java API. Nó cung cấp các cấu trúc dữ liệu và thuật toán để lưu trữ và thao tác với các nhóm đối tượng một cách hiệu quả.

## Collections Framework là gì?

**Collections Framework** là một kiến trúc thống nhất để biểu diễn và thao tác với các collections (tập hợp). Nó bao gồm:

- **Interfaces**: Định nghĩa các contract cho các loại collections
- **Implementations**: Các class cụ thể triển khai các interfaces
- **Algorithms**: Các phương thức tĩnh để thao tác với collections

## Các Interface chính

### 1. Collection Interface

Interface gốc cho tất cả collections:

```java
Collection<String> collection = new ArrayList<>();
collection.add("Java");
collection.add("Python");
collection.add("JavaScript");

System.out.println("Size: " + collection.size()); // Size: 3
```

### 2. List Interface

Danh sách có thứ tự, cho phép phần tử trùng lặp:

```java
List<String> list = new ArrayList<>();
list.add("First");
list.add("Second");
list.add(0, "Zero"); // Thêm vào vị trí đầu

for (String item : list) {
    System.out.println(item);
}
```

### 3. Set Interface

Tập hợp không có thứ tự, không cho phép phần tử trùng lặp:

```java
Set<String> set = new HashSet<>();
set.add("Apple");
set.add("Banana");
set.add("Apple"); // Bị bỏ qua vì đã tồn tại

System.out.println(set.size()); // 2
```

### 4. Map Interface

Cấu trúc key-value:

```java
Map<String, Integer> map = new HashMap<>();
map.put("Java", 1995);
map.put("Python", 1991);
map.put("JavaScript", 1995);

System.out.println(map.get("Java")); // 1995
```

## Các Implementation phổ biến

### ArrayList

Danh sách động, truy cập nhanh theo index:

```java
ArrayList<String> arrayList = new ArrayList<>();
arrayList.add("Element 1");
arrayList.add("Element 2");
arrayList.remove(0); // Xóa phần tử đầu

// Truy cập nhanh
String first = arrayList.get(0);
```

**Ưu điểm:**
- Truy cập nhanh O(1) theo index
- Thêm/xóa ở cuối nhanh

**Nhược điểm:**
- Thêm/xóa ở giữa chậm O(n)

### LinkedList

Danh sách liên kết, thêm/xóa nhanh:

```java
LinkedList<String> linkedList = new LinkedList<>();
linkedList.addFirst("First");
linkedList.addLast("Last");
linkedList.add(1, "Middle");

linkedList.removeFirst();
```

**Ưu điểm:**
- Thêm/xóa nhanh O(1) ở bất kỳ vị trí nào

**Nhược điểm:**
- Truy cập chậm O(n) theo index

### HashMap

Bảng băm, truy cập nhanh theo key:

```java
HashMap<String, String> hashMap = new HashMap<>();
hashMap.put("name", "Java");
hashMap.put("version", "17");

String name = hashMap.get("name");
boolean exists = hashMap.containsKey("version");
```

**Đặc điểm:**
- Truy cập O(1) trung bình
- Không đảm bảo thứ tự

### TreeMap

Map được sắp xếp theo key:

```java
TreeMap<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Zebra", 1);
treeMap.put("Apple", 2);
treeMap.put("Banana", 3);

// Tự động sắp xếp: Apple, Banana, Zebra
for (String key : treeMap.keySet()) {
    System.out.println(key);
}
```

## So sánh các Collections

| Collection | Thứ tự | Trùng lặp | Null | Thread-safe |
|------------|--------|-----------|------|-------------|
| ArrayList | Có | Có | Có | Không |
| LinkedList | Có | Có | Có | Không |
| HashSet | Không | Không | Có | Không |
| TreeSet | Có (sắp xếp) | Không | Không | Không |
| HashMap | Không | Key không | Có | Không |
| TreeMap | Có (sắp xếp) | Key không | Key không | Không |

## Best Practices

✅ **Chọn đúng Collection cho nhu cầu:**

```java
// Cần thứ tự và truy cập nhanh
List<String> list = new ArrayList<>();

// Cần không trùng lặp
Set<String> set = new HashSet<>();

// Cần key-value
Map<String, Object> map = new HashMap<>();
```

✅ **Sử dụng Generics:**

```java
// Đúng
List<String> list = new ArrayList<>();

// Sai - Raw type
List list = new ArrayList();
```

✅ **Sử dụng Iterator để duyệt:**

```java
List<String> list = new ArrayList<>();
Iterator<String> iterator = list.iterator();

while (iterator.hasNext()) {
    String item = iterator.next();
    // Xử lý item
}
```

✅ **Sử dụng Collections utility class:**

```java
List<Integer> numbers = Arrays.asList(3, 1, 4, 1, 5);
Collections.sort(numbers);
Collections.reverse(numbers);
int max = Collections.max(numbers);
```

## Ứng dụng thực tế

Collections Framework được sử dụng trong:

- 📊 **Data Processing**: Xử lý dữ liệu từ database
- 🎮 **Game Development**: Quản lý danh sách đối tượng
- 🌐 **Web Development**: Lưu trữ session, cache
- 📱 **Mobile Apps**: Quản lý danh sách items
- 🔍 **Search Algorithms**: Cấu trúc dữ liệu cho tìm kiếm

## Kết luận

Java Collections Framework là công cụ mạnh mẽ và linh hoạt cho việc quản lý dữ liệu. Hiểu rõ các đặc điểm và cách sử dụng của từng collection sẽ giúp bạn viết code hiệu quả và tối ưu hơn.

## Tài liệu tham khảo

- [Oracle Java Collections Tutorial](https://docs.oracle.com/javase/tutorial/collections/)
- Java API Documentation: `java.util.Collection`
- Java API Documentation: `java.util.Map`

---

**Bạn có câu hỏi về Collections Framework? Hãy để lại comment bên dưới!** 💬

