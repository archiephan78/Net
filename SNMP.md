## Simple Network Management Protocol|(SNMP)

I. **SNMP là gì?**

  - SNMP là một giao thức tầng ứng dụng quy định bởi IAB trong RFC1157 để trao đổi thông tin quản lý giữa các thiết bị mạng.

  - SNMP là một tập hợp các giao thức không chỉ cho phép kiểm tra tài nguyên và giám sát lưu lượng các thiết bị mạng như router,switch hay server đang vận hành mà còn hỗ trợ vận hành các thiết bị này một cách tối ưu. Ngoài ra SNMP còn cho phép quản lý các thiết bị mạng từ xa/

  - Giao thức SNMP được thiết kế để cung cấp một phương thức đơn giản để quản lý tập trung mạng TCP/IP. Nếu bạn muốn quản lý các thiết bị từ 1 vị trí tập trung, giao thức SNMP sẽ vận chuyển dữ liệu từ client (thiết bị mà bạn đang giám sát) đến server nơi mà dữ liệu được lưu trong log file nhằm phân tích dễ dàng hơn

  - SNMP dùng để quản lý tức là có thể theo dõi, có thể lấy thông tin, có thể được thông báo, và có thể tác động để hệ thống hoạt động như ý muốn.

  - Ví dụ một số khả năng của SNMP:

    - Theo dõi tốc độ đường truyền của một router/máy chủ, biết được tổng số byte đã truyền/nhận.

    - Lấy thông tin máy chủ đang có bao nhiêu ổ cứng, mỗi ổ cứng còn trống bao nhiêu

    - Tự động nhận cảnh báo khi switch có 1 port bị down

    - Điều khiển shutdown các port trên switch.

  - Có 2 nhân tố chính trong SNMP:  manager và agent. Các SNMP agent sẽ giữ một sơ sở dữ liệu, được gọi là Management Information Base (MIB), trong đó chứa các thông tin khác nhau về hoạt động của thiết bị mà agent đang giám sát. Phần mềm quản trị SNMP Manager sẽ thu thập thông tin này qua giao thức SNMP.

  <img src=https://i.imgur.com/GDrwXY8.jpg>

  - Ưu điểm khi thiết kế hệ thống quản trị với SNMP sẽ giúp đơn giản hóa các quá trình quản lý các thành phần trong mạng, giảm chi phí triển khai. SNMP được thiết kế có thể hoạt động độc lập với các kiến trúc và cơ chế của các thiết bị hỗ trợ SNMP. Các thiết bị khác nhau có hoạt động khác nhau nhưng đáp ứng SNMP là giống nhau.

  - SNMP bao gồm một bộ các tiêu chuẩn để quản lý mạng, bao gồm một giao thức lớp ứng dụng, một giản đồ cơ sở dữ liệu, và một tập các data objects

II. **SNMP hoạt động như thế nào**:

  - Có 2 phương pháp giám sát là poll và alert

    - Poll: Manager sẽ thường xuyên hỏi thông tin của agent. Nếu manager không hỏi thì agent không trả lời

    - Alert: Mỗi khi agent xảy ra event nào đó thì nó sẽ tự động gửi thông báo cho manager

  - SNMP sử dụng UDP (User Datagram Protocol) làm giao thức truyền tải thông tin giữa manager và các agent. Việc sử dụng UDP, thay vì TCP, bởi vì UDP là phương thức truyền mà trong đó hai đầu thông tin không cần thiết lập kết nối trứơc khi dữ liệu được trao đổi (connectionless), thuộc tính này phù hợp trong điều kiện mạng gặp trục trặc, hư hỏng... cần ưu tiên về mặt tốc độ.

  - Trong các ứng dụng của SNMP, một hoặc nhiều máy tính quản trị được gọi là các máy managers có nhiệm vụ giám sát hoặc quản lý một nhóm máy chủ hoặc thiết bị trên mạng máy tính. Mỗi hệ thống được quản lý được gọi là một agent báo cáo thông tin thông qua SNMP cho máy manager.

  <img src= https://i.imgur.com/IVTEvyT.png >

  - Hệ thống SNMP bao gồm 2 thành phần chính:

    - Manager

    - Agent

  - SMP Manager là máy được config để nhận và xử lý thông tin từ Agent gửi tới. Manager có thể  yêu cầu truy vấn đến các Agents với các thông tin chính xác.

  - Agent thu thập thông tin của client và lưu trữ chúng ở định dạng có thể query được

  - MIB (Management Information base) là một cấu trúc được định nghĩa theo thứ bậc, lưu trữ thông tin có thể được truy vấn hay thiết lập. Cấu trúc MIB được hiểu là cây phân cấp từ trên xuống dưới. Mỗi nhánh được fork ra được dán nhãn với cả 1 số nhận dạng(bắt đầu bằng 1) và 1 chuỗi xác định.

  <img src=https://i.imgur.com/AXhVG5I.png>

  - Các node có 1 Object ID duy nhất. ví dụ sysUPtime có OID là 1.3.6.1.2.1.1.3.0

- SNMP protocol Command

  - SNMP có các phương thức quản lý nhất định và các phương thức này được định dạng bởi các gói tin PDU (Protocol Data Unit). Các manager và agent sử dụng PDU để trao đổi với nhau.

  - Get : Get message gửi bởi manager tới agent để yêu cầu giá trị của 1 OID cụ thể. được trả lời với gói Response

  - GetNext: Manager yêu cầu object tiếp theo trong MIB.

  - Set: Manager gửi đến 1 agent để thay đổi giá trị được gửi bởi 1 biến trên agent.Điều này có thể sử dụng để kiểm soát thông tin cấu hình hoặc thay đổi trạng thái máy chủ từ xa.

  - Response: gửi bởi agent, dùng để gửi bất kỳ thông tin nào mà manager yêu cầu

  - Trap: Được gửi từ agent đến manager. Là các thông báo không đồng bộ ở chỗ chúng không được yêu cầu bởi manager. Chủ yếu sử dụng để truyền thông tin cần mornitor. Có 2 loại trap là generic trap và specific trap:

    - generic trap: được quy định trong các chuẩn SNMP

    - specific trap : được người dùng định nghĩa

  - SNMP chạy trên UDP. cấu trúc 1 bản tin SNMP bao gồm version,community và data(PDU).

  <img src=https://i.imgur.com/Kh6J4FN.jpg>


  III. **Cấu hình và cài đặt Cacti**

  - Môi trường cài đặt : VMware

  - Mô hình:

  <img src=https://i.imgur.com/839fvj5.png>

1. ** Config máy agent**

  - Cài đặt các package:

  ```
  apt-get -y install snmp snmpd snmp-mibs-downloader
  ```

  - Config file /etc/snmp/snmpd.conf

  ```
  # line 15: comment out
  #agentAddress udp:127.0.0.1:161
  # line 17: uncomment
  agentAddress udp:161,udp6:[::1]:161
  # line 49: uncomment and change to any comunity name you like
  rocommunity public localhost
  # line 51: comment out
  #rocommunity public default -V systemonly
  # line 59: uncomment and change to any comunity name & change access permission
  rocommunity public 10.0.0.0/24

  ```
  - Restart service snmpd

  ```
  systemctl restart snmpd
  ```

2.  ** Config máy manager**

  - Tiến hành cài đặt snmp và cacti:

  ```
  apt-get -y install cacti snmp snmpd snmp-mibs-downloader php-mysql php-snmp rrdtool
  ```

  - Commend dòng mibs trong snmp.conf để chấp nhận Manager import MIB file

  ```
  root@agent:~# vim /etc/snmp/snmp.conf
  #mibs
  ```
  - Config file /etc/snmp/snmp.conf

  ```
  # line 4: comment out
  #mibs
  ```
  - Config /etc/snmp/snmpd.conf

  ```
  # line 49: uncomment and change to any comunity name you like
  rocommunity Serverworld localhost
  # line 51: comment out
  #rocommunity public default -V systemonly
  ```
  - Restart Service

  - Trên giao diên web 10.0.0.135/cacti tiến hành config tạo device thông tin như sau

  <img src=https://i.imgur.com/oxY9uRm.png>

  - Vào graph tree tạo tree items

  <img src=https://i.imgur.com/nZgRoex.png>

  - Vào new graph tạo Graph và kết quả ta đã có graph ( config hiện thị ở thanh toolbar ngay trên)

  <img src= https://i.imgur.com/y2c7QgM.png >

3. Cấu hình arlet đến mail

  - Cài đặt các plugin :

  ```
  $ wget http://docs.cacti.net/_media/plugin:settings-v0.71-1.tgz
  $ wget http://docs.cacti.net/_media/plugin:thold-v0.5.0.tgz
  $ mv plugin:settings-v0.71-1.tgz settings-v0.71-1.tgz
  $ mv plugin:thold-v0.5.0.tgz thold-v0.5.0.tgz
  $ tar zxf settings-v0.71-1.tgz
  $ tar zxf thold-v0.5.0.tgz
  ```

  - Vào giao diện web chạy các plugin ấy, vào setting/ tab mail/dns config như sau

  <img src=https://i.imgur.com/VGb5eFe.png>

  - Save lại và thử test  email

  <img src=https://i.imgur.com/ktr30uc.png>
