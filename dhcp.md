<h2 style="text-align: center;markdown ="1> Dynamic Host Configuration Protocol</h2>

1. **DHCP là gì?**

  Dynamic Host Configuration Protocol (DHCP - giao thức cấu hình động máy chủ) là một giao thức cho phép cấp phát địa chỉ IP một cách tự động cùng với các cấu hình liên quan khác như subnet mark và gateway mặc định. Máy tính được cấu hình một cách tự động vì thế sẽ giảm việc can thiệp vào hệ thống mạng. Nó cung cấp một database trung tâm để theo dõi tất cả các máy tính trong hệ thống mạng. Mục đích quan trọng nhất là tránh trường hợp hai máy tính khác nhau lại có cùng địa chỉ IP.

  Nếu không có DHCP, các máy có thể cấu hình IP thủ công (cấu hình IP tĩnh). Ngoài việc cung cấp địa chỉ IP, DHCP còn cung cấp thông tin cấu hình khác, cụ thể như DNS. Hiện nay DHCP có 2 version: cho IPv4 và IPv6.

  DHCP được định nghĩa trong RFC1531, DHCP là 1 giao thức chạy theo mo hình client/server. DHCP là một giao thức có nguồn gốc từ RARP sau giao thức RARP phát triển lên BOOTP và cuối cùng được cải tiến lên DHCP do nhu cầu cải tiến kĩ thuật mạng.RARP là một giao thức mạng sơ khai được dùng bởi các máy client để yêu cầu có một địa chỉ Ipv4 để sử dụng cho mục đích liên lạc với các máy khác trong trạm. (thời kì đầu, khi mới có địa chỉ IP và các máy bắt đầu dùng địa chỉ IP để liên lạc thay cho địa chỉ MAC). Hạn chế của RARP là giao thức lớp 2, chỉ cấp địa chỉ IP và không cấp thêm một thông tin nào khác, là giao thức cấp địa chỉ tĩnh sơ khai và còn cần nhiều sự tương tác của người quản trị mạng khi phải cấu hình thông tin trên RARP server trước.
 BOOTP được dùng để cấu hình cho các máy trạm khởi động mà không cần đĩa cứng. BOOTP thi hành các công việc sau:
      - Tìm kiếm địa chỉ IP cho chính nó
      - Tìm kiếm IP của BOOTP server
      - Nạp một file khởi động từ server vào bộ nhớ
      - Bắt đầu khởi động
      - Nó vẫn còn một số hạn chế là không cấp được địa chỉ IP động khi mà nhu cầu cấp địa chỉ động trở thành rõ rệt hơn bao giờ hết khi Internet thực sự khởi đầu cất cánh vào cuối thập niên 1990 và việc gán địa chỉ IP tĩnh và dùng mãi cho mỗi máy để chúng kết nối vào mạng là một phí phạm.

  DHCP khai thác ưu điểm của giao thức truyền tin và các kỹ thuật khai báo cấu hình được định nghĩa trong BOOTP, trong đó có khả năng tìm kiếm và gán địa chỉ IP cho nhiều mạng con. Theo đó quá trình tương tác giữa DHCP client và server diễn ra thông qua các gói tin
      - DHCP dicover
      - DHCP offer
      - DHCP Request
      - DHCP Acknowledgement.


2. **Cơ chế cấp phát DHCP**

    DHCP gồm 3 cơ chế phân bổ địa chỉ khác nhau:
      - Manual Allocation:
      Một địa chỉ IP cụ thể được cấp phát trước cho một thiết bị duy nhất bởi người quản trị. DHCP chỉ truyền IP tới các thiết bị đó (hiểu như là server, router, gateway, ... ). Nó cũng thích hợp cho các thiết bị khác mà vì lý do gì phải có một địa chỉ IP cố định ổn định.
      - Automatic Allocation:DHCP tự động gán một địa chỉ IP vĩnh viễn với một thiết bị, chọn từ một pool IP có sẵn. Sử dụng trong trường hợp có đủ địa chỉ IP cho mỗi thiết bị có thể kết nối vào mạng, nhưng mà thiết bị không thực sự cần quan tâm đến địa chỉ mà nó sử dụng. Khi một địa chỉ được gán cho một client, thiết bị sẽ tiếp tục sử dụng nó. Automatic Allocation được coi là một trường hợp đặc biệt của Dynamic Allocation – dùng trong trường hợp các giới hạn thời gian sử dụng các địa chỉ IP của một client gần như là “mãi mãi”.
      - Dynamic Allocation: DHCP gán một địa chỉ IP từ một pool các địa chỉ trong một khoảng thời gian hạn chế được lựa chọn bởi server, hoặc cho đến khi client nói với DHCP server là nó không cần địa chỉ này nữa. 
      


3. **Các loại bản tin DHCP**
      - DHCP discover

    Đầu tiên máy client sẽ gửi đi đi 1 gói tin quảng bá tên là DHCP discover nhằm yêu cầu cho việc lấy các thông tin cấu hình như IP address, Subnet mask, Defaut Gateway, Preferred DNS,.. Lúc này vì client chưa có IP nên nó sẽ dùng 1 địa chỉ soucer là 0.0.0.0 đồng thời nó cũng không biết địa chỉ của DHCP server nên nó sẽ gửi đến địa chỉ broadcast là 255.255.255.255 và sau đó gói tin DHCP discover này sẽ quảng bá đi toàn mạng. Gói tin này chứa 1 địa chỉ MAC, ngoài ra nó chứa tên của máy client.

      - DHCP Offer

    Sau khi nhận được gói tin DHCP discover của client nếu có 1 DHCP Server hợp lệ thì nó sẽ trả lời lại bằng 1 gói DHCP Offer. Gói tin này chứa 1 địa chỉ IP đề nghị cho trong 1 khoảng thời gian nhất định, sau 50% thời gian nó sẽ tự động thu hồi IP nếu client không sử dụng. Gói tin này còn kèm theo địa chỉ MAC của client được cấp, 1 subnet mask và địa chỉ IP của DHCP Server đã cấp phát. Trong thời gian này server sẽ không cấp phát địa chỉ IP vừa đề nghị cho 1 client nào khác.

      - DHCP Request

    Máy client sau khi nhận được gói tin DHCP Offer trên mạng sẽ tiến hành phản hồi lại bằng 1 gói tin DHCP Request để  chấp nhận lời đề nghị đó. Điều này giúp cho việc các gói tin còn lại không được chấp nhận sẽ được các server rút lại và cấp phát cho các client khác.

      - DHCP Acknowledgement

    Khi DHCP Server nhận được gói tin DHCP Request, nó sẽ trả lời bằng 1 gói tin DHCP ack nhằm mục đích thông báo rằng là nó đã chấp nhận cho DHCP client đó địa chỉ IP này. Gói tin bao gồm địa chỉ IP và các thông tin cấu hình khác (DNS,gateway,...)
      
      -	DHCP NAK 
      
    Nếu địa chỉ IP không thể được sữ dụng bởi client bởi vì nó không còn giá trị nữa hoặc được sử dụng hiện tại bởi một máy tính khác, DHCP Server đáp ứng với gói DHCP Nak, và Client phải bắt đầu tiến trình thuê bao lại. Bất cứ khi nào DHCP Server nhận được yêu cầu từ một địa chỉ IP mà không có giá trị theo các Scope mà nó được định cấu hình với, nó gửi thông điệp DHCP Nak đối với Client.
    
      -	DHCP DECLINE 
      
     Khi client nhận được thông tin cấu hình từ DHCP server, nhưng có thể xảy ra vấn đề là IP mà DHCP server cấp đã bị sử dụng bởi một thiết bị khác thì nó gửi gói DHCP Decline đến các Server và Client phải bắt đầu tiến trình thuê bao lại từ đầu.
     
      -	DHCP RELEASE 
      
     Một DHCP Client khi không còn nhu cầu sử dụng IP hiện tại nữa nó sẽ  gửi một gói DHCP Release đến server quản lý để giải phóng địa chỉ IP và xoá bất cứ hợp đồng thuê bao nào đang tồn tại.
     
      -	DHCP INFORM 
      
     Các thiết bị không sử dụng DHCP để lấy địa chỉ IP vẫn có thể sử dụng khả năng cấu hình khác của nó. Một client có thể gửi một bản tin DHCP INFORM để yêu cầu bất kì máy chủ có sẵn nào gửi cho nó các thông số để mạng hoạt động. DHCP server đáp ứng với các thông số yêu cầu – được điền trong phần tùy chọn của DHCP trong bản tin DHCP ACK.

    Tất cả việc trao đổi thong tin giữa client và server sử dụng UDP trên cổng 67 và 68.
    
 4.**Mô hình lab**
 
 
 <img src= http://i.imgur.com/4WY5n44.png >
 
 - Môi truờng : VMware 
 - DHCP Server : Ubuntu 16.04 Server , NIC host only 1 ( ens33), IP 192.168.1.1
 - DHCP Client : Ubuntu 16.04 Server , NIC host only 1 ( ens33)
 
    4.1. Cấu hình trên DHCP server
    
    - Cài đặt isc-dhcp server
    ```
    sudo apt-get install isc-dhcp-server
    ```
    
    - Cấu hình config file tại /etc/deafault/isc-dhcp-server chuyển mục INTERFACE thành tên NIC của server
    
    ```
    [...]
    INTERFACES="ens3"
    ```
    
    - Cấu hình cấp phát cụ thể tại /etc/dhcp/dhcpd.conf
    
    ```
    [...]
    # A slightly different configuration for an internal subnet.
     subnet 192.168.1.0 netmask 255.255.255.0 {
     range 192.168.1.20 192.168.1.30;
     option domain-name-servers dhcp.lan;
     option domain-name "dhcp";
     option routers 192.168.1.1;
     option broadcast-address 192.168.1.255;
     default-lease-time 600;
     max-lease-time 7200;
     }
    [...]
    ```
    - Reset service
    
    ```
    sudo systemctl restart isc-dhcp-server
    ```
    
    4.2. Cấp phát dhcp cho client
    
     - Khởi động máy client và kiểm tra cấu hình dhcp
       
       
      ```
       ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.21  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::4cd6:decb:514c:5bd1  prefixlen 64  scopeid 0x20<link>
        ether 74:de:2b:74:1f:36  txqueuelen 1000  (Ethernet)
        RX packets 2263335  bytes 3055792204 (3.0 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1046597  bytes 140896828 (140.8 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
      ```
