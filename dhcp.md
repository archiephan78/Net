<h2 style="text-align: center;markdown ="1> Dynamic Host Configuration Protocol</h2>

1. **DHCP là gì?**

  Dynamic Host Configuration Protocol (DHCP - giao thức cấu hình động máy chủ) là một giao thức cho phép cấp phát địa chỉ IP một cách tự động cùng với các cấu hình liên quan khác như subnet mark và gateway mặc định. Máy tính được cấu hình một cách tự động vì thế sẽ giảm việc can thiệp vào hệ thống mạng. Nó cung cấp một database trung tâm để theo dõi tất cả các máy tính trong hệ thống mạng. Mục đích quan trọng nhất là tránh trường hợp hai máy tính khác nhau lại có cùng địa chỉ IP.

  Nếu không có DHCP, các máy có thể cấu hình IP thủ công (cấu hình IP tĩnh). Ngoài việc cung cấp địa chỉ IP, DHCP còn cung cấp thông tin cấu hình khác, cụ thể như DNS. Hiện nay DHCP có 2 version: cho IPv4 và IPv6.

  DHCP được định nghĩa trong RFC1531, DHCP là 1 giao thức chạy theo mo hình client/server. DHCP là một giao thức có nguồn gốc từ BOOTP, được dùng để cấu hình cho các máy trạm khởi động mà không cần đĩa cứng. BOOTP thi hành các công việc sau:
      - Tìm kiếm địa chỉ IP cho chính nó
      - Tìm kiếm IP của BOOTP server
      - Nạp một file khởi động từ server vào bộ nhớ
      - Bắt đầu khởi động

  DHCP khai thác ưu điểm của giao thức truyền tin và các kỹ thuật khai báo cấu hình được định nghĩa trong BOOTP, trong đó có khả năng tìm kiếm và gán địa chỉ IP cho nhiều mạng con. Theo đó quá trình tương tác giữa DHCP client và server diễn ra thông qua các gói tin
      - DHCP dicover
      - DHCP offer
      - DHCP Request
      - DHCP Acknowledgement.


2. **Cơ chế cấp phát DHCP**

      - DHCP discover

    Đầu tiên máy client sẽ gửi đi đi 1 gói tin quảng bá tên là DHCP discover nhằm yêu cầu cho việc lấy các thông tin cấu hình như IP address, Subnet mask, Defaut Gateway, Preferred DNS,.. Lúc này vì client chưa có IP nên nó sẽ dùng 1 địa chỉ soucer là 0.0.0.0 đồng thời nó cũng không biết địa chỉ của DHCP server nên nó sẽ gửi đến địa chỉ broadcast là 255.255.255.255 và sau đó gói tin DHCP discover này sẽ quảng bá đi toàn mạng. Gói tin này chứa 1 địa chỉ MAC, ngoài ra nó chứa tên của máy client.

      - DHCP Offer

    Sau khi nhận được gói tin DHCP discover của client nếu có 1 DHCP Server hợp lệ thì nó sẽ trả lời lại bằng 1 gói DHCP Offer. Gói tin này chứa 1 địa chỉ IP đề nghị cho trong 1 khoảng thời gian nhất định, sau 50% thời gian nó sẽ tự động thu hồi IP nếu client không sử dụng. Gói tin này còn kèm theo địa chỉ MAC của client được cấp, 1 subnet mask và địa chỉ IP của DHCP Server đã cấp phát. Trong thời gian này server sẽ không cấp phát địa chỉ IP vừa đề nghị cho 1 client nào khác.

      - DHCP Request

    Máy client sau khi nhận được gói tin DHCP Offer trên mạng sẽ tiến hành phản hồi lại bằng 1 gói tin DHCP Request để  chấp nhận lời đề nghị đó. Điều này giúp cho việc các gói tin còn lại không được chấp nhận sẽ được các server rút lại và cấp phát cho các client khác.

      - DHCP Acknowledgement

    Khi DHCP Server nhận được gói tin DHCP Request, nó sẽ trả lời bằng 1 gói tin DHCP ack nhằm mục đích thông báo rằng là nó đã chấp nhận cho DHCP client đó địa chỉ IP này. Gói tin bao gồm địa chỉ IP và các thông tin cấu hình khác (DNS,gateway,...)

    Tất cả việc trao đổi thong tin giữa client và server sử dụng UDP trên cổng 67 và 68.
