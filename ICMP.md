### Internet Control Message Protocol 

1. **Giới thiệu**

   - Internet Control Message Protocol (viết tắt là ICMP), là một giao thức của gói Internet Protocol. Giao thức này được các 
 thiết bị mạng như router dùng để gửi đi các thông báo lỗi chỉ ra một dịch vụ có tồn tại hay không, hoặc một địa chỉ host hay 
 router có tồn tại hay không. ICMP cũng có thể được sử dụng để chuyển tiếp các thông điệp truy vấn. Giao thức này được đánh số 
 1. ICMP khác với các giao thức vận chuyển như TCP và UDP ở chỗ nó không thường được sử dụng để trao đổi dữ liệu giữa các hệ 
 thống, cũng không thường xuyên được sử dụng bởi các ứng dụng mạng của người dùng cuối (với ngoại lệ của một số công cụ chẩn 
 đoán như ping và traceroute).
 
  -  ICMP sử dụng IP để làm cơ sở thông tin liên lạc bằng cách giải thích chính nó như là một lớp giao thức cao hơn, thông điệp
  ICMP được đóng gói trong các gói tin IP.

  - ICMP nhận ra một số tình trạng lỗi, nhưng không làm IP trở thành một giao thức đáng tin cậy.

  - ICMP phân tích sai sót trong mỗi gói IP, trừ các đối tượng mà mang một thông điệp ICMP.

  - Thông điệp ICMP không được gửi để trả lời các gói tin gởi tới các điểm đến mà có các địa chỉ multicast hoặc broadcast.
   Thông điệp ICMP chỉ trả lời một địa chỉ IP định rõ.
2. **Hoạt động của ICMP**   

  - IP không có cơ chế để biết data mà nó đã gửi có đến được đích chưa, nên mới sinh ra cái gọi là Internet Control Message 
  Protocol (ICMP). ICMP không phải để giải quyết cái thuộc tính unreliability vốn có của IP mà ICMP message có nhiệm vụ đơn 
  giản là báo cho sender biết việc gửi data đi đã có vấn đề.
  
  - Ví dụ: host A gỏi một datagram tới host Z, nhưng trên đường tới đích, có thể do một trong số các nguyên nhân sau sẽ làm 
  cho gói tin không đến được đúng đích:
  
     + Các thiết bị trung gian như routing protocol chưa đúng ... chúng được gọi là unreachable network
     + Cấu hình TCP/IP chưa đúng về địa chỉ, subnetmask hay default gateway... chúng được gọi là unreachable host
     + Host dích không hỗ trợ upper-layer protocol. Được gọi là unreachable protocol
     + Host đich không hỗ trợ loại dịch vụ cần truy câp. Gọi là unreachable port/socket
     
  - .Khi đó thiết bị trung gian (router) nơi sảy ra vấn đề sẽ gửi lại một gói tin trong đó có ICMP message chỉ dành cho sender 
  để thông báo về nguyên nhân. Các thiết bị trung gian khác không nhận được message trên và hoàn toàn không biết là có vấn đề 
  trên đường truyền. 
  
  - Có nhiều loại ICMP message và mỗi loại mang môt thông điệp lỗi cụ thể khác nhau. Kiểu message được nhận ra nhờ format dữ 
  liệu của message đó.
  
  - Các loại ICMP message được encap với header đều có 3 trường chung:
  
      + Type (8bit): Chỉ kiểu của ICMP message. Chi tiet
          - 0: Echo reply
          - 3: Destination unreachable
          - 4: Source quench
          - 5: Redirect
          - 8: Echo
          - 9: Router advertisement
          - 10: Router solicitation
          - 11: Time exceeded
          - 12: Parameter problem
          - 13: Timestamp request
          - 14: Timestamp reply
          - 15: Information request (obsolete)
          - 16: Information reply (obsolete)
          - 17: Address mask request
          - 18: Address mask reply
          - 30: Traceroute
          - 31: Datagram conversion error
          - 32: Mobile host redirect
          - 33: Ipv6 Where-Are-You
          - 34: Ipv6 I-Am-Here
          - 35: Mobile registration request
          - 36: Mobile registration reply
          - 37: Domain name request
          - 38: Domain name reply
          - 39: SKIP
          - 40: Photuris
      
        + Code (8bit): Bổ sung thông tin thêm cho Type (ví dụ với Type = 0/8 code=0 -> echo message)
        + Checksum (16bit)
    
    Sau đó là các trường option khác. Và sau header là data.
    
 3.**Các loại ICMP message thường thấy**
 
    
    3.1 ICMP echo messages

  - Có hai loại là echo request và echo reply message tương ứng với Với các trường:
        + Type = 0 -> echo request, code = 0
        + Type = 8 -> echo reply, code = 0

  - Ngoài ra còn có 2 trường (size là 16bit/field) là ID và sequence Number dùng để nhận biết giữ các cặp reply/request.

    3.2. ICMP Destination Unreachable message

  - Như đã nói về Destination Unreachable. Nếu bị Destination Unreachable, thiết bị trung gian sẽ gửi một Destination 
    Unreachable message về sender.

  - Destination Unreachable có nhiều loại ứng với các nghuyên nhân khác nhau và chúng sẽ có các cặp giá trị code khác nhau:
    Ví dụ:
      + Type = 3, code = 0 -> Network Unreachable
      + Type = 3, code = 1 -> Host Unreachable
      + Type = 3, code = 2 -> Protocol Unreachable
      + Type = 3, code = 3 -> Port Unreachabl


    3.3. ICMP Parameter Problem message

  - Vấn đề sảy ra khi có một vài error trong header của datagram (ở một vài octet) và không thể chuyển nó đi tiếp được. Khi 
  đó thiêt bị trung gian gửi một ICMP Parameter Problem message cho sender với các trường như sau.

      + Type = 12
      + Thêm một trường Poiter (8bit) để chỉ vị trí của octet lỗi
