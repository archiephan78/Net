# **TÌM HIỂU GIAO THỨC ARP**

# 1. Giới thiệu giao thức ARP

## 1.1. Đặt vấn đề

Trong một hệ thống mạng máy tính, có 2 địa chỉ được gán cho máy tính là: 

- **Địa chỉ logic**: là địa chỉ của các giao thức mạng như IP, IPX, ... Loại địa chỉ này chỉ mang tính chất tương đói, có thể thay đổi theo sự cần thiết của người dùng. Các địa chỉ này thường được phân thành 2 phần riêng biệt là phần địa chỉ mạng và phần địa chỉ máy. Cách đánh địa chỉ như vậy nhắm giúp cho việc tìm ra các đường kết nối từ hệ thống mạng này sang hệ thống mạng khác dễ dàng hơn. 

- **Địa chỉ vật lý**: hay còn gọi là địa chỉ **MAC - Medium Access Control address** là địa chỉ 48 bit, dùng để định danh duy nhất do nhà cung cấp gán cho mỗi thiết bị. Đây là loại địa chỉ phẳng, không phân lớp, nên rất khó dùng để định tuyến.

Trên thực tế, các card mạng (NIC) chỉ có thể kết nối với nhau theo địa chỉ MAC, địa chỉ cố định và duy nhất của phần cứng.

**=>** Do vậy phải có một cơ chế để ánh xạ địa chỉ logic - lớp 3 sang địa chỉ vật lý - lớp 2 để các thiết bị có thể giao tiếp với nhau.

Từ đó, ta có giao thức phân giải địa chỉ ARP - Address Resolution Protocol giải quyết vấn đề trên.
