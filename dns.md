<h2 style="text-align: center;markdown ="1> Domain Name System</h2>

1. **DNS là gì?**

  Hệ thống tên miền (DNS) là 1 giao thức phổ biến trên mạng Internet chạy trên port 53(UDP), về căn bản là 1 hệ thống giúp cho việc chuyển đổi các tên miền mà con người dễ ghi nhớ( dạng ký tự) sang địa chỉ IP vật lý ( dạng số) tương ứng của tên miền đó. DNS giúp liên kết với các trang thiết bị mạng cho mục đích định vị và địa chỉ hóa các thiết bị trên Internet.

    DNS được định nghĩa chính thức trong chuẩn RFC1034 và RFC1035, DNS giúp mạng Internet thân thiện hơn với người dùng. Tổ chức ICANN có trách nhiệm điều hành hệ thống root, chia thành các kiểu tên miền có dạng .com, .org, .edu,... Mỗi quốc gia đều cử ra một dại diện điều hành tên miền cấp cao của quốc gia mình, ví dụ tại VN tên miền .vn do VNNIC kiểm soát.
2.  **Cấu trúc DNS**

  Hệ thống tên trong DNS được sắp xếp theo mô hình phân cấp và cấu trúc cây logic được gọi là DNS namespace. Ví dụ :
```sequence
                  .root
       +-------------+--------------+
       |             |              |
      .com          .edu            .net
       |
  .microsoft
-------+-------
|             |
.asia        .eu
```   
Hệ thống tên miền được phân thành nhiều cấp
  - Gốc ( Doamin root), nó là đỉnh cuả nhánh cây của tên miền. Nó có thể biểu diễn đơn giản chỉ là dấu .
  - Tên miền cấp một(Top-level-domain) gồm vài ký tự xác định 1 quốc gia, khu vực hoặc 1 tổ chức.(.com, .edu)
  - Tên miền cấp hai ( Second-level-domanin) Nó rất đa dạng, có thể là tên công ty, tổ chức hay 1 cá nhân
  - Tên miền cấp nhỏ hơn ( sub domain) Chia thêm ra của tên miền cấp 2 trở xuống thường được sử dụng như chi nhánh,phòng ban của 1 công ty.

  DNS có khả năng tra vấn các DNS server khác để có một cái tên đã được phân giải. DNS server của mỗi tên miền thường có 2 việc khác biệt. Thứ nhất chịu trách nhiệm phân giải tên từ các máy bên trong miền về các địa chỉ Internet, cả bên trong lẫn bên ngoài miền nó quản lý. Thứ hai, chúng trả lời các DNS server bên ngoài đang cố gắng phân giải những tên miền nó quản lý. DNS server có khả năng ghi nhớ lại những tên vừa phân giải. Để dùng cho những yêu cầu phân giải lần sau. Số lượng những tên phân giải được lưu lại tùy thuộc vào quy mô của từng DNS.
3. **DNS server**

  DNS server là một cơ sở dữ liệu chứa các thông tin về vị trị của các DNS domain và phân giải các truy vấn xuất phát từ client.

  DNS server lưu thông tin của Zone, truy vấn và trả kết quả cho DNS client, chạy DNS service.

  Các bản ghi DNS được phân loại như sau:
   - **A** : Bản ghi A xác định địa chỉ IPv4 của tài nguyên mạng . Vdu như bản ghi:

    ``` www IN A 1.2.3.4
    ```
    trong tên miền chungpt.vccloud.vn định nghĩa www.chungpt.vccloud.vn được định nghĩa duy nhất tại địa chỉ 1.2.3.4

   - **CNAME**: Bản ghi canonical name xác định một định danh khác hay còn gọi là bí danh(alias) sẽ được phân giải đến khi tìm thấy bản ghi A. Ví dụ :
   ``` www IN CNAME www.chungpt.vccloud.vn
   ```
   trong tên miền chungpt.vn định nghĩa định danh duy nhất www.chungpt.vn là bí danh cho www.chungpt.vccloud.vn

   - **MX**: bản ghi MX( mail exchange) xác định tên tài nguyên và danh sách máy chủ mail theo thứ tự ưu tiên cho tên miền đó. Ví dụ bản ghi
   ```
       chungpt.vccloud.vn IN MX 10 mailsrv1
       chungpt.vccloud.vn IN MX 20 mailsrv2
   ```
   xác định mailsrv1.chungpt.vccloud.vn là máy chủ mail được ưu tiên gửi đến đầu tiên và tiếp theo sau đó là mailsrv2

   - **NS**: bản ghi name server xác định authorritative name server của domain. Ví dụ bản ghi:
       ``` chungpt.vccloud.vn IN NS ns1.chungpt.vccloud.vn
       ```
   - **PTR** : Bản ghi PTR trỏ 1 địa chỉ IP đến một bản ghi A trong chế độ ngược
   - **TTL** : là thời gian cache của bản ghi DNS trên một máy chủ tên miền trước khi máy chủ đó tìm kiếm 1 phiên bản cập nhật.
   - **Bản ghi SOA** : Thông thường mỗi tên miền sẽ sử dụng một cặp DNS nào đó để trỏ về  1 hoặc nhiều máy chủ DNS, và ở đây các máy chủ DNS các máy chủ DNS có trách nhiệm cung cập thông tin bản ghi DNS của hệ thống cho tên miền này để nó hoạt động. SOA đươc coi như dấu hiệu nhận biêt của hệ thống tên miền này

   <img src=http://i.imgur.com/gzBaNVO.jpg>
 
 3.**Moo hình lab**
 
  - Môi truờng : VMware

  - DNS Server : Ubuntu 16.04 Server , NIC host only 1 ( ens33), IP 192.168.1.2

  - DNS Client : Ubuntu 16.04 Server , NIC host only 1 ( ens33), IP 192.168.1.10

<img src =http://i.imgur.com/QA3JeRv.png >
