---
title: "Multithreading trong Java - Lập trình đa luồng"
date: 2025-12-13
draft: false
description: "Tìm hiểu về Multithreading trong Java - cách tạo và quản lý nhiều thread"
tags: ["Java", "Multithreading", "Thread", "Concurrency", "Synchronization"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/multithreading.jpg"
  alt: "Multithreading trong Java"
  caption: "Multithreading trong Java"
---

## Giới thiệu

Multithreading cho phép chương trình Java thực thi nhiều tác vụ đồng thời, tận dụng tối đa sức mạnh của CPU đa nhân. Đây là kỹ năng quan trọng cho việc phát triển ứng dụng hiệu năng cao.

## Thread là gì?

**Thread** là một luồng thực thi độc lập trong một chương trình. Một chương trình Java có thể có nhiều thread chạy đồng thời, mỗi thread thực thi một phần công việc.

## Tạo Thread

### Cách 1: Extend Thread class

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Thread: " + i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

// Sử dụng
MyThread thread = new MyThread();
thread.start();
```

### Cách 2: Implement Runnable interface

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Runnable: " + i);
        }
    }
}

// Sử dụng
Thread thread = new Thread(new MyRunnable());
thread.start();
```

### Cách 3: Lambda Expression (Java 8+)

```java
Thread thread = new Thread(() -> {
    for (int i = 0; i < 5; i++) {
        System.out.println("Lambda: " + i);
    }
});
thread.start();
```

## Thread Lifecycle

```
NEW → RUNNABLE → RUNNING → BLOCKED/WAITING → TERMINATED
```

```java
Thread thread = new Thread(() -> {
    // RUNNABLE
    System.out.println("Thread đang chạy");
});

thread.start(); // Chuyển sang RUNNABLE
// Thread chạy (RUNNING)
// Khi hoàn thành → TERMINATED
```

## Synchronization

### Vấn đề Race Condition

```java
class Counter {
    private int count = 0;
    
    public void increment() {
        count++; // Không thread-safe
    }
    
    public int getCount() {
        return count;
    }
}
```

### Giải pháp: Synchronized Method

```java
class Counter {
    private int count = 0;
    
    public synchronized void increment() {
        count++; // Thread-safe
    }
    
    public synchronized int getCount() {
        return count;
    }
}
```

### Synchronized Block

```java
public void increment() {
    synchronized (this) {
        count++;
    }
}
```

## Thread Pool với ExecutorService

### Sử dụng ThreadPoolExecutor

```java
ExecutorService executor = Executors.newFixedThreadPool(5);

for (int i = 0; i < 10; i++) {
    final int taskId = i;
    executor.submit(() -> {
        System.out.println("Task " + taskId + " đang chạy");
    });
}

executor.shutdown();
```

### Các loại Thread Pool

```java
// Fixed Thread Pool
ExecutorService fixedPool = Executors.newFixedThreadPool(5);

// Cached Thread Pool
ExecutorService cachedPool = Executors.newCachedThreadPool();

// Single Thread Executor
ExecutorService singlePool = Executors.newSingleThreadExecutor();

// Scheduled Thread Pool
ScheduledExecutorService scheduledPool = Executors.newScheduledThreadPool(3);
```

## Future và Callable

### Callable với return value

```java
Callable<String> task = () -> {
    Thread.sleep(2000);
    return "Kết quả từ thread";
};

ExecutorService executor = Executors.newSingleThreadExecutor();
Future<String> future = executor.submit(task);

try {
    String result = future.get(); // Chờ kết quả
    System.out.println(result);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Thread Communication

### Wait và Notify

```java
class SharedResource {
    private boolean available = false;
    
    public synchronized void produce() {
        while (available) {
            try {
                wait(); // Chờ consumer
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        available = true;
        notify(); // Thông báo consumer
    }
    
    public synchronized void consume() {
        while (!available) {
            try {
                wait(); // Chờ producer
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        available = false;
        notify(); // Thông báo producer
    }
}
```

## Concurrent Collections

### Thread-safe Collections

```java
// ConcurrentHashMap
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("key", 1);

// CopyOnWriteArrayList
CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>();
list.add("item");

// BlockingQueue
BlockingQueue<String> queue = new LinkedBlockingQueue<>();
queue.put("item");
String item = queue.take(); // Chờ đến khi có item
```

## Best Practices

✅ **Sử dụng Thread Pool thay vì tạo thread mới:**

```java
// Sai
for (int i = 0; i < 100; i++) {
    new Thread(() -> {
        // work
    }).start();
}

// Đúng
ExecutorService executor = Executors.newFixedThreadPool(10);
for (int i = 0; i < 100; i++) {
    executor.submit(() -> {
        // work
    });
}
```

✅ **Tránh deadlock:**

```java
// Tránh lock nhiều object cùng lúc
// Luôn lock theo cùng một thứ tự
```

✅ **Sử dụng volatile cho shared variables:**

```java
private volatile boolean running = true;

public void stop() {
    running = false;
}
```

✅ **Sử dụng Atomic classes:**

```java
AtomicInteger counter = new AtomicInteger(0);
counter.incrementAndGet();
```

## Ứng dụng thực tế

Multithreading được sử dụng trong:

- 🌐 **Web Servers**: Xử lý nhiều request đồng thời
- 🎮 **Game Development**: Xử lý game logic và rendering
- 📊 **Data Processing**: Xử lý dữ liệu song song
- 🔍 **Search Engines**: Tìm kiếm đa luồng
- 💬 **Chat Applications**: Xử lý nhiều kết nối cùng lúc

## Kết luận

Multithreading là công cụ mạnh mẽ để tăng hiệu năng ứng dụng. Tuy nhiên, cần cẩn thận với synchronization và race conditions để tránh bugs khó debug.

## Tài liệu tham khảo

- [Oracle Java Concurrency Tutorial](https://docs.oracle.com/javase/tutorial/essential/concurrency/)
- Java API Documentation: `java.lang.Thread`
- Java API Documentation: `java.util.concurrent`

---

**Bạn có câu hỏi về Multithreading? Hãy để lại comment bên dưới!** 💬

