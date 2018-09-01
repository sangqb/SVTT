# Tổng quan về Software Defined Networking và OpenvSwitch
---
## 1. Software Defined Networking (SDN) và OpenFlow
### 1.1. Giới thiệu
Software Defined Networking (SDN) hay mạng điều khiển bằng phần mềm hoạt động dựa trên cơ chế tách bạch việc kiểm soát một luồng mạng với luồng dữ liệu. SDN định nghĩa ra một lớp phần mềm đứng giữa các phần tử mạng và người quản trị mạng (là người cấu hình và cài đặt chúng). Lớp phần mềm này cung cấp cho người quản trị mạng khả năng điều khiển các thiết bị mạng của họ thông qua một giao diện phần mềm thay vì phải tự cấu hình phần cứng hoặc điều chỉnh các yếu tố vật lý của thiết bị mạng. 
SDN tách riêng luồng điều khiển (control plane) với luồng dữ liệu (và data plane). Điều này cho phép luồng các gói dữ liệu đi qua mạng được kiểm soát theo lập trình. Control plane được tách ra từ các thiết bị vật lý và chuyển đến các bộ điều khiển (trong lớp phần mềm). Các bộ điều khiển tương tác với các thiết bị mạng vật lý thông qua giao thức Open Flow. 

### 1.3. Kiến trúc SDN
Kiến trúc SDN gồm 3 lớp riêng biệt: lớp ứng dụng (Application Layer), lớp điều khiển (Control Layer), lớp cơ sở hạ tầng - phần thiết bị (Infrastructure Layer). Các lớp này liên kiết với nhau thông qua giao thức OpenFlow và các API.
![](images/1-OVS-Introduction/1-DSN-Architecture.png)

## 2. OpenFlow
## 3. OpenvSwitch (OVS)
### 3.1. Giới thiệu
- OvS là một trong những thành phần quan trọng hỗ trợ SDN (Software Defined Networking - Công nghệ mạng điều khiển bằng phần mềm).
- OvS là phần mềm mã nguồn mở hỗ trợ giao thức Openflow.
- OvS được sử dụng với các hypervisor để kết nối giữa các máy ảo trên một host vật lý và các máy ảo giữa các host vật lý khác nhau qua mạng.
- OvS cũng được sử dụng trên một số thiết bị chuyển mạch vật lý (Ví dụ: Switch Pica8).
- Tính năng:
    - Hỗ trợ VLAN tagging và chuẩn 802.1q trunking
    - Hỗ trợ STP (spanning tree protocol)
    - Hỗ trợ LACP (Link Aggregation Control Protocol)
    - Hỗ trợ port mirroring (SPAN, RSPAN)
    - Hỗ trợ Flow export (sử dụng các giao thức sflow và netflow)
    - Hỗ trợ các giao thức đường hầm (GRE, VXLAN, IPSEC, tunneling)
    - Hỗ trợ kiểm soát QoC

### 3.2. Cài đặt OpenvSwitch trên Ubuntu 18.04 LTS