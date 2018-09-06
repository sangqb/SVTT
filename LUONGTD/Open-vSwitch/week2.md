# Kiến trúc của OpenvSwitch

## [1. Kiến trúc tổng quan](#general)
## [2. Kiến trúc chi tiết](#detail)
---
## <a name="general"></a> 1. Kiến trúc tổng quan
![](images/2-OVS-Architecture/ovs_arch.jpg)
- Nhắc lại là OVS thường được sử dụng để kết nối các máy ảo (VM/container) trong một host. OVS quản lý cả các port vật lý (eth0, eth1) và các port ảo (ví dụ như các port của VMs).
- Ba khối thành phần chính của OVS:
	- __vsswitchhd__: Là daemon chạy trên user space.
	- __ovsdb-server__: Là database server của OVS chạy trên user space
	- __kernel module__ (data path): Là module thuộc kernel space, thực hiện công việc chuyển tiếp gói tin.		

## <a name="detail"></a> 2. Kiến trúc chi tiết
