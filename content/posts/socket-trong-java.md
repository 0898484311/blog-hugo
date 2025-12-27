---
title: "Socket trong Java là gì?"
date: 2025-12-13
draft: false
description: "Tìm hiểu về Socket trong Java - cách giao tiếp giữa client và server qua mạng"
tags: ["Java", "Socket", "Network Programming", "TCP/IP"]
categories: ["Lập trình mạng"]
showtoc: true
cover:
  image: "/images/Socket.jpg"
  alt: "Socket Programming in Java"
  caption: "Socket Programming trong Java"
---

## Giới thiệu


Socket trong Java là một công cụ mạnh mẽ cho phép các ứng dụng giao tiếp với nhau qua mạng. Đây là nền tảng cơ bản cho việc phát triển các ứng dụng client-server, chat applications, web servers và nhiều ứng dụng mạng khác.

## Socket là gì?

**Socket** là một điểm cuối (endpoint) của kết nối hai chiều giữa hai chương trình chạy trên mạng. Nó hoạt động như một "cổng" cho phép dữ liệu đi vào và ra khỏi một ứng dụng.

### Các thành phần chính

Trong Java, lập trình socket sử dụng các class chính sau:

- **`ServerSocket`**: Dùng ở phía server để lắng nghe kết nối từ client
- **`Socket`**: Dùng ở cả client và server để gửi/nhận dữ liệu
- **`InputStream` / `OutputStream`**: Để đọc và ghi dữ liệu qua socket

## Kiến trúc Client-Server

{{< figure src="/images/ClientSever.png" alt="Client-Server Architecture" align="center" width="300" >}}

```
┌─────────────┐         Socket Connection         ┌─────────────┐
│   Client    │ <──────────────────────────────> │   Server    │
│             │                                   │             │
│   Socket    │                                   │ ServerSocket│
│             │                                   │    Socket   │
└─────────────┘                                   └─────────────┘
```

## Ví dụ cơ bản

### Server Side

```java
import java.io.*;
import java.net.*;

public class SimpleServer {
    public static void main(String[] args) {
        try {
            // Tạo ServerSocket lắng nghe ở port 8080
            ServerSocket serverSocket = new ServerSocket(8080);
            System.out.println("Server đang chờ kết nối...");
            
            // Chấp nhận kết nối từ client
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client đã kết nối!");
            
            // Tạo BufferedReader để đọc dữ liệu từ client
            BufferedReader in = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream())
            );
            
            // Đọc dữ liệu từ client
            String message = in.readLine();
            System.out.println("Nhận từ client: " + message);
            
            // Tạo PrintWriter để gửi dữ liệu về client
            PrintWriter out = new PrintWriter(
                clientSocket.getOutputStream(), true
            );
            out.println("Server đã nhận: " + message);
            
            // Đóng kết nối
            clientSocket.close();
            serverSocket.close();
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### Client Side

```java
import java.io.*;
import java.net.*;

public class SimpleClient {
    public static void main(String[] args) {
        try {
            // Kết nối đến server tại localhost:8080
            Socket socket = new Socket("localhost", 8080);
            
            // Gửi dữ liệu đến server
            PrintWriter out = new PrintWriter(
                socket.getOutputStream(), true
            );
            out.println("Xin chào từ client!");
            
            // Đọc phản hồi từ server
            BufferedReader in = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );
            String response = in.readLine();
            System.out.println("Nhận từ server: " + response);
            
            // Đóng kết nối
            socket.close();
            
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Luồng hoạt động

{{< figure src="/images/Socket.jpg" alt="Socket Flow Diagram" align="center" width="300" >}}

1. **Server** tạo `ServerSocket` và lắng nghe ở một port cụ thể
2. **Client** tạo `Socket` và kết nối đến server
3. Server chấp nhận kết nối bằng `accept()`
4. Cả hai bên có thể gửi/nhận dữ liệu qua `InputStream` và `OutputStream`
5. Đóng kết nối khi hoàn thành

## Các loại Socket

### TCP Socket (Stream Socket)
- Kết nối đáng tin cậy, có đảm bảo thứ tự
- Sử dụng `Socket` và `ServerSocket`
- Phù hợp cho: HTTP, FTP, Email

### UDP Socket (Datagram Socket)
- Kết nối không đảm bảo, nhanh hơn
- Sử dụng `DatagramSocket` và `DatagramPacket`
- Phù hợp cho: Video streaming, Online games

## Best Practices

✅ **Luôn đóng socket**: Sử dụng try-with-resources hoặc finally block

```java
try (Socket socket = new Socket("localhost", 8080)) {
    // Sử dụng socket
} catch (IOException e) {
    e.printStackTrace();
}
```

✅ **Xử lý exception**: Luôn bắt và xử lý `IOException`

✅ **Timeout**: Thiết lập timeout cho socket để tránh treo

```java
socket.setSoTimeout(5000); // 5 giây
```

✅ **Threading**: Sử dụng multi-threading cho server để xử lý nhiều client

## Ứng dụng thực tế

Socket programming được sử dụng trong:
- 🌐 Web servers (HTTP)
- 💬 Chat applications
- 🎮 Online games
- 📧 Email clients
- 📡 Real-time data streaming
- 🔌 IoT devices communication

## Kết luận

Socket trong Java là công cụ cơ bản nhưng mạnh mẽ cho lập trình mạng. Hiểu rõ cách hoạt động của socket sẽ giúp bạn phát triển các ứng dụng mạng hiệu quả và đáng tin cậy.

## Tài liệu tham khảo

- [Oracle Java Networking Tutorial](https://docs.oracle.com/javase/tutorial/networking/)
- Java API Documentation: `java.net.Socket`
- Java API Documentation: `java.net.ServerSocket`

---

**Bạn có câu hỏi hoặc muốn chia sẻ kinh nghiệm về Socket programming? Hãy để lại comment bên dưới!** 💬
