# Một vài ghi chép
---
## 0.0 OVS:
- Wireless base stations generally only allow packets with the source MAC address of NIC that completed the initial handshake. Therefore, without MAC rewriting, only a single device can  communicate over a single wireless link.
This isn't specific to Open vSwitch, it's enforced by the access point, so the same problems will show up with the Linux bridge or any other way to do bridging. 

## 0.1. daemon
- Daemon là chương trình chạy nền giống như các service trên Window, có thể tắt mở tự động mà không ảnh hưởng đến giao diện người dùng. Các daemon process thường gặp như là web server hay là database.

## 0.2. kernel
- Kernel là khái niệm chỉ những phần mềm, ứng dụng mức thấp (low-level) trong hệ thống, có khả năng thay đổi linh hoạt để phù hợp với phần cứng. Chúng tương tác với tất cả các ứng dụng và hoạt động trong chế độ usermode, cho phép các quá trình khác - hay còn gọi là server, nhận thông tin từ các thành phần khác qua Inter-Process-Communication (IPC).
- Các file kernel này, trong Ubuntu chúng đưọc lưu trữ tại thư mục /boot/ và đặt tên theo vmlinuz-version. Khi bộ nhớ ảo bắt đầu được phát triển để thực hiện các tác vụ đa luồng, tiền tố vm sẽ được đặt vào đầu các file kernel để phân biệt khả năng hỗ trợ công nghệ ảo hóa. Kể từ đó, Linux kernel được gọi là vmlinux, nhưng hệ thống kernel này đã phát triển quá nhanh, lớn hơn so với dung lượng bộ nhớ boot chuẩn của hệ điều hành, vì vậy những kernel này đã được nén theo chuẩn zlib,... chúng được gọi chung là zImage.
