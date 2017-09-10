# **TÌM HIỂU GIAO THỨC ARP**

# 1. Giới thiệu giao thức ARP

## 1.1. Đặt vấn đề

Trong một hệ thống mạng máy tính, có 2 địa chỉ được gán cho máy tính là: 

- **Địa chỉ logic**: là địa chỉ của các giao thức mạng như IP, IPX, ... Loại địa chỉ này chỉ mang tính chất tương đói, có thể thay đổi theo sự cần thiết của người dùng. Các địa chỉ này thường được phân thành 2 phần riêng biệt là phần địa chỉ mạng và phần địa chỉ máy. Cách đánh địa chỉ như vậy nhắm giúp cho việc tìm ra các đường kết nối từ hệ thống mạng này sang hệ thống mạng khác dễ dàng hơn. 

- **Địa chỉ vật lý**: hay còn gọi là địa chỉ **MAC - Medium Access Control address** là địa chỉ 48 bit, dùng để định danh duy nhất do nhà cung cấp gán cho mỗi thiết bị. Đây là loại địa chỉ phẳng, không phân lớp, nên rất khó dùng để định tuyến.

Trên thực tế, các card mạng (NIC) chỉ có thể kết nối với nhau theo địa chỉ MAC, địa chỉ cố định và duy nhất của phần cứng.

 Do vậy phải có một cơ chế để ánh xạ địa chỉ logic - lớp 3 sang địa chỉ vật lý - lớp 2 để các thiết bị có thể giao tiếp với nhau.

Từ đó, ta có giao thức phân giải địa chỉ ARP - Address Resolution Protocol giải quyết vấn đề trên.

## 1.2. ARP là gì?

– ARP là phương thức phân giải địa chỉ động giữa địa chỉ lớp network và địa chỉ lớp datalink. Quá trình thực hiện bằng cách: một thiết bị IP trong mạng gửi một gói tin local broadcast đến toàn mạng yêu cầu thiết bị khác gửi trả lại địa chỉ phần cứng ( địa chỉ lớp datalink ) hay còn gọi là Mac Address của mình.

– ARP là giao thức lớp 2 - Data link layer trong mô hình OSI và là giao thức lớp Link layer trong mô hình TCP/IP.

– Ban đầu ARP chỉ được sử dụng trong mạng Ethernet để phân giải địa chỉ IP và địa chỉ MAC. Nhưng ngày nay ARP đã được ứng dụng rộng rãi và dùng trong các công nghệ khác dựa trên lớp hai.

# 2. Cấu trúc bản tin ARP

Kích thước bản tin ARP là 28 byte, được đóng gói trong frame Ethernet II nên trong mô hình OSI, ARP được coi như là giao thức lớp 3 cấp thấp.

Cấu trúc bản tin ARP được mô tả như hình sau:

<img src="http://imgur.com/ZmKo5pU.jpg">

- **Hardware type:** 

  - Xác định kiểu bộ giao tiếp phần cứng cần biết.

  - Xác định với kiểu Ethernet giá trị 1.

- **Protocol type:**

  - Xác định kiểu giao thức cấp cao (layer 3) máy gửi sử dụng để giao tiếp.

  - Giao thức dành cho IP có giá trị 0x0800.

- **Hardware address length:** Xác định độ dài địa chỉ vật lý (tính theo đơn vị byte). Địa chỉ MAC nên giá trị của nó sẽ là 6.

- **Protocol address length:** Xác định độ dài địa chỉ logic được sử dụng ở tầng trên (layer 3). Tùy thuộc vào IP sử dụng mà có giá trị khác nhau, hiện tại IPv4 được sử dụng rộng rãi nên trường này sẽ có giá trị là 4 (byte).

- **Operation code:** Xác định loại bản tin ARP mà máy gửi gửi. Có một số giá trị phổ biến:

  - 1 : bản tin ARP request.

  - 2 : bản tin ARP rely.

  - 3 : bản tin RARP request.

  - 4 : bản tin RARP reply.

- **Sender hardware address (SHA):** Xác định địa chỉ MAC máy gửi. 

  - Trong bản tin ARP request: trường này xác định địa chỉ MAC của host gửi request.

  - Trong bản tin ARP reply: trường này xác định địa chỉ MAC của máy host mà máy gửi bên trên muốn tìm kiếm.

- **Sender protocol address (SPA):** Xác định địa chỉ IP máy gửi.

- **Target hardware address (THA):** Xác định địa chỉ MAC máy nhận mà máy gửi cần tìm.

  - Trong bản tin ARP request: Trường này chưa được xác định (nên sẽ để giá trị là: 00:00:00:00:00:00)

  - Trong bản tin ARP reply: Trường này sẽ điền địa chỉ của máy gửi bản tin ARP request.

- **Target protocol address (PTA):** Xác định địa chỉ IP máy gửi (máy cần tìm).
