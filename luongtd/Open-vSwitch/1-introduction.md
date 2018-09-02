# Tổng quan về Software Defined Networking và OpenvSwitch
---
## 1. Software Defined Networking và OpenFlow
Software Defined Networking (SDN) hay mạng điều khiển bằng phần mềm hoạt động dựa trên cơ chế tách bạch việc kiểm soát một luồng mạng với luồng dữ liệu. SDN định nghĩa ra một lớp phần mềm đứng giữa các phần tử mạng và người quản trị mạng (là người cấu hình và cài đặt chúng). Lớp phần mềm này cung cấp cho người quản trị mạng khả năng điều khiển các thiết bị mạng của họ thông qua một giao diện phần mềm thay vì phải tự cấu hình phần cứng hoặc điều chỉnh các yếu tố vật lý của thiết bị mạng. 
SDN tách riêng luồng điều khiển (control plane) với luồng dữ liệu (và data plane). Điều này cho phép luồng các gói dữ liệu đi qua mạng được kiểm soát theo lập trình. Control plane được tách ra từ các thiết bị vật lý và chuyển đến các bộ điều khiển (trong lớp phần mềm). Các bộ điều khiển tương tác với các thiết bị mạng vật lý thông qua giao thức Open Flow. 

Kiến trúc SDN gồm 3 lớp riêng biệt: lớp ứng dụng (Application Layer), lớp điều khiển (Control Layer), lớp cơ sở hạ tầng - phần thiết bị (Infrastructure Layer). Các lớp này liên kiết với nhau thông qua giao thức OpenFlow và các API.
![](images/1-OVS-Introduction/1-SDN-Arch.png)
- Lớp ứng dụng: Là các ứng dựng kinh doanh đưọc triển khai trên mạng, được kết nối tới lớp điều khiển thông qua các API, cung cấp khả năng cho phép lớp ứng dụng lập trình lại (cấu hình lại) mạng (điều chỉnh các tham số trễ, băng thông, định tuyến,...) thông qua lớp điều khiển.
- Lớp điều khiển: Là nơi tập trung các bộ điều khiển thực hiện việc điều khiển cấu hình mạng theo các yêu cầu từ lớp ứng dụng và khả năng của mạng. Các bộ điều khiển này có thể là các phần mềm được lập trình.
- Lớp cơ sở hạ tầng: Là các thiết bị mạng thực tế (vật lý hay ảo hóa) thực hiện việc chuyển tiếp	gói tin theo sự điều khiển của lớp điều khiển. Một thiết bị mạng có thể hoạt động theo sự điều khiển của nhiều bộ điều khiển khác nhau, điều này giúp tăng cường khả năng ảo hóa của mạng.
## 2. OpenFlow
OpenFlow là tiêu chuẩn đầu tiên, cung cấp khả năng truyền thông giữa các giao diện của lớp điều khiển và lớp chuyển tiếp trong kiến trúc SDN. OpenFlow cho phép truy cập trực tiếp và điều khiển một mặt phẳng chuyển tiếp của các thiết bị mạng như switch, router, cả thiết bị vật lý và thiết bị ảo, do đó giúp di chuyển phần điều khiển mạng ra khỏi các thiết bị chuyển mạch thực tế tới phần mềm điều khiển trung tâm. Các quyết định về các luồng traffic sẽ được quyết định tập trung tại OpenFlow Controller giúp đơn giản hóa việc quản trị cấu hình trong toàn hệ thống. Một thiết bị OpenFlow bao gồm ít nhẩt ba thành phần:
- Source Channel: Kênh nối thiết bị tới bộ điều khiển (Controller), cho phép các lệnh và gói tin được gửi giữa bộ điều khiển và thiết bị.
- OpenFlow Protocol: giao thức cung cấp phương thức tiêu chuẩn và mở cho một bộ điều khiển truyền thông với thiết bị.
- Flow Table: một liên kết hành động với mỗi luồng, giúp thiết bị xử lý các luồng.
![](images/1-OVS-Introduction/1-OpenFlow.png)
## 3. OpenvSwitch
### 3.1. Giới thiệu
- OpenvSwitch (OVS) là một dự án phần mềm mã nguồn mở về chuyển mạch ảo đa lớp hỗ trợ giao thức Openflow.
- OVS là một trong những thành phần quan trọng hỗ trợ SDN. 
- Mục đích chính của OVS là cung cấp lớp chuyển mạch cho môi trường ảo hóa phần cứng. OVS hỗ trợ nhiều giao thức và tiêu chuẩn được sử dụng trong hệ thống chuyển mạch thông thường. OVS hỗ trợ nhiều công nghệ ảo hóa dựa trên nền tảng Linux như Xen/XenServer, KVM và VirtualBox.
- OVS được sử dụng với các hypervisor để kết nối giữa các máy ảo trên một host vật lý và các máy ảo giữa các host vật lý khác nhau qua mạng.
![](images/1-OVS-Introduction/1-OVS-overview.png)
- OVS hỗ trợ các tính năng sau:  
    - VLAN tagging và chuẩn 802.1q trunking
    - STP (spanning tree protocol)
    - LACP (Link Aggregation Control Protocol)
    - Port mirroring (SPAN, RSPAN)
    - Flow export (sử dụng các giao thức sflow và netflow)
    - Các giao thức đường hầm (GRE, VXLAN, IPSEC, tunneling)
    - Kiểm soát QoC
![](images/1-OVS-Introduction/1-OVS-overview2.png)
### 3.2. Các thành phần chính của OpenvSwitch:
- ovs-vswitchd: thực hiện chuyển đổi các luồng chuyển mạch
- ovsdb-server: là một lightweight database server, cho phép ovs-vswitchd thực hiện các truy vấn đến cấu hình
- ovs-dpctl: công cụ để cấu hình các switch kernel module
- ovs-vsctl: tiện ích để truy vấn và cập nhật cấu hình ovs-vswitchd
- ovs-appctl: tiện ích gửi command để chạy OVS

### 3.3. Cài đặt OpenvSwitch trên Ubuntu 18.04 LTS
#### 3.3.1. Building OpenvSwitch Debian packages
  1. Cài đặt các gói "build-essential" và fakeroot"
```sh
$ apt-get install build-essential fakeroot
```
  2. Download và giải nén OVS source distribution và cd vào top level directory
![](images/1-OVS-Introduction/build0.png)
  3. Cài đặt các gói phụ thuộc (build dependencies) được liệt kê trong "Build-Depends:" ở gần đầu file debian/control. Ta có thể cài đặt với apt-get install.
  Kiểm tra xem đã đủ các gói phụ thuộc chưa bằng cách chạy dpkg-checkbuilddeps ở cấp cao nhất trong thư mục OVS. Nếu đã cài đặt tất cả các phụ thuộc đúng cách, dpkg-checkbuilddeps sẽ thoát mà không cần in bất kỳ thứ gì. Nếu ta quên cài đặt một số phụ thuộc, nó sẽ cho ta biết mục nào còn thiếu.
![](images/1-OVS-Introduction/build3-0.png)
![](images/1-OVS-Introduction/build3-1.png)
![](images/1-OVS-Introduction/build3-2.png)
  4. Build package:
 ```sh
$ fakeroot debian/rules binary
 ```
  Lệnh này sẽ tiến hành một serial build chạy các unit tests. Quá trình này sẽ mất khoảng 8 đến 10 phút. Ta thể chạy một bản build song song nhanh hơn:
  ```sh
  DEB_BUILD_OPTIONS='parallel=8' fakeroot debian/rules binary
  ```
  Nếu gấp, thậm chí có thể bỏ qua các unit tests:
  ```sh
  DEB_BUILD_OPTIONS='parallel=8 nocheck' fakeroot debian/rules binary
  ```
  ```Chú ý:``` Có một vài cạm bẫy trong hệ thống packaging Building của Debian, thỉnh thoảng, bạn có thể thấy rằng trong một cây mà bạn đã sử dụng trong một thời gian, lệnh build ở trên thoát ngay lập tức mà không thực sự build bất cứ thứ gì. Để khắc phục sự cố, chạy:
  ```sh
$ fakeroot debian/rules clean
  ```
  hoặc bắt đầu từ một bản sao mới của source tree.

  5. File .deb được tạo ra sẽ nằm ở thư parent directory của OVS source distribution.
![](images/1-OVS-Introduction/build4.png)
![](images/1-OVS-Introduction/build5.png)

#### 3.3.2. Cài đặt .deb Packages
Các lệnh này áp dụng để cài đặt từ các gói Debian mà bạn tự xây dựng, như được mô tả trong phần trước. Trong trường hợp này, sử dụng lệnh như ```dpkg -i``` để cài đặt các tệp .deb mà bạn tạo. Ta sẽ phải tự cài đặt bất kỳ phụ thuộc bị thiếu nào.
![](images/1-OVS-Introduction/install.png)