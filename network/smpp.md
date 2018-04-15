SMPP Protocol
===
![SMPP Model](./images/smpp_model.png)

- SMPP (Short Message Peer to Peer) là một chuẩn giao thức mở được thiết kế để áp dụng trong các hệ thống về nhắn tin SMS (Short Message Service). 
- SMPP là giao thức giúp vẫn chuyện các Short Message giữa các ESME (External Short Message Entities) và các Message Center thông qua một interface giúp xử lý giao tiếp dữ liễu một cách linh hoạt.
- Muốn sử dụng được SMPP cần phải đăng ký và host từ một service provider, ở đây có thể là một SMSC (Short Message Service Centre). Sau khi đã đăng ký, ta sẽ có được một sô thông tin từ service provider như: IP và port của SMSC, username (system id) và password.
- Ứng dụng sử dụng SMPP sẽ theo mô hình client và server, SMPP Server sẽ listen trên port đã đc cung cấp từ SMSC, SMPP Client sẽ kết nối đến SMPP Server thông qua address có dạng (smpp://[SMSC's IP]:[SMSC's port]).
- Khi cài đặt SMPP Server ta sẽ sử dụng các thư viện về network trong một số ngôn ngữ, thường mỗi ngôn ngữ sẽ có một thư viện (có thể open source) viếc sẵn cho SMPP.
- Các gói tin của SMPP vận chuyện gọi là PDU (Protocal Dât Units).