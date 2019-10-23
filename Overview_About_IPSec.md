# IPSec

### Tổng quan

IPSec (Internet Protocol Security) bao gồm một hệ thống các giao thức để bảo mật quá trình truyền thông tin trên nền tảng Internet Protocol (IP). Bao gồm xác thực **và/hoặc** mã hóa **(Authenticating and/or Encrypting)** cho mỗi gói IP (IP packet) trong quá trình truyền thông tin.

Giao thức IPSec được làm việc tại tầng Network Layer - layer 3 của mô hình OSI. Các giao thức bảo mật khác như SSL, TLS và SSH, được thực hiện từ tầng transport layer trở lên.

###### Vai trò của IPSec

* Cho phép xác thực hai chiều, trước và trong quá trình truyền tải dữ liệu
* Mã hóa đường truyền giữa hai máy tính khi được gửi qua một mạng
* Bảo vệ gói dữ liệu IP và phòng ngự các cuộc tấn công mạng không bảo mật
* IPSec bảo vệ các lưu lượng mạng bằng việc sử dụng mã hóa và đánh dấu dữ liệu
* Cho phép định nghĩa các loại lưu lượng mà IPSec sẽ kiểm tra và cách các lưu lượng đó sẽ được bảo mật và mã hóa như thế nào

###### Các tính năng của IPSec

* *Bảo mật (Confidentiality)*

  Đảm bảo dữ liệu được an toàn, tránh những cuộc tấn công bằng cách thay đổi nội dung hoặc đánh cắp dữ liệu quan trọng. Việc bảo vệ dữ liệu được thực hiện bằng các thuật toán mã hóa như DES, 3DES và AES

* *Tính toàn vẹn dữ liệu (Data integrity)*

  Đảm bảo dữ liệu không bị thay đổi trong suốt quá trình trao đổi bằng cách sử dụng thuật toán băm (hash) để kiểm tra xem dữ liệu bên trong có bị thay đổi hay không, những gói tin bị phát hiện đã bị thay đổi sẽ bị loại bỏ. Những thuật toán băm phổ biến là: MD5 hoặc SHA-1

* *Tính xác thực (Authentication)*

  Xác định có kết nối đến đúng người cần kết nối hay không, tính năng này không tồn tại một mình mà phụ thuộc vào toàn vẹn dữ liệu. Việc chứng thực dựa vào kỹ thuật: **Pre-shared key, RSA-encryption, RSA-signature**

* *Tránh trùng lặp (Anti-replay)*

  Đảm bảo gói tin không bị trùng lặp bằng việc đánh số thứ tự. Gói tin nào trùng lặp sẽ bị loại bỏ

###### Các ứng dụng của IPSec

* Bảo vệ kết nối từ các mạng chi nhánh đến mạng trung tâm thông qua Internet
* Bảo vệ kết nối truy cập từ xa (Remote Access)
* Thiết lập các kết nối Intranet và Extranet
* Nâng cao tính bảo mật của các giao dịch thương mại điện tử

### Kiến trúc IPSec

###### Kiến trúc

IPSec là một giao thức phức tạp, dựa trên nền của nhiều kỹ thuật cơ sở khác nhau như mật mã, xác thực, trao đổi khóa. Về kiến trúc thì IPSec được xây dựng cơ bản dựa trên các thành phần cơ bản sau:

 <img src="/images/Ipsec_architecture.jpg" height="500">

* Giao thức ESP (Encapsulating Security Header): ESP cung cấp sự bảo mật, toàn vẹn dữ liệu, chứng thực nguồn gốc dữ liệu và chống tấn công Anti-reply
* Giao thức AH (Authentication Header): AH cũng cung cấp cơ chế kiểm tra toàn vẹn dữ liệu, chứng thực dữ liệu, cũng như là chống tấn công. Nhưng điểm khác biệt giữa AH và ESP là AH không cung cấp các cơ chế bảo mật dữ liệu, header của AH đơn giản hơn ESP
* Thuật toán mã hóa (Encryption Algorithm): Định nghĩa các thuật toán mã hóa và giải mã được sử dụng trong IPSec. IPSec chủ yếu dựa vào các thuật toán mã hóa đối xứng
* Thuật toán xác thực (Authentication Algorithm): Định nghĩa các thuật toán xác thực thông tin sử dụng trong AH và ESP
* DOI (Domain of Interpretation): Định nghĩa môi trường thực thi IPSec. Vì IPSec không phải là một công nghệ riêng biệt mà là một tập hợp các cơ chế, giao thức khác nhau , mỗi loại trong đó đều có các cơ chế hoạt động khác nhau
* Quản lý khóa (Key management): Mô tả các cơ chế quản lý và trao đổi khóa trong IPSec

###### Khung giao thức IPSec

Khung giao thức được sử dụng trong IPSec:

<img src="/images/khunggiaothuc.png" height="300">

Một số tính năng được khuyến khích sử dụng khi làm việc với IPSec:

| Giao thức bảo mật | Thuật toán mã hóa | Toàn vẹn dữ liệu | Phương pháp xác thực | Quản lý khóa | Chính sách an ninh |
| ----------------- | ----------------- | ---------------- | -------------------- | ------------ | ------------------ |
| AH, ESP           | DES, 3DES         | MD5, SHA-1       | RSA                  | DH, CA       | IKE, ISAKMP        |

###### Các giao thức IPSec

Để trao đổi và thỏa thuận các thông số nhằm tạo nên một môi trường bảo mật đầu cuối, IPSec dùng ba giao thức:

* IKE (Internet Key Exchange) dùng để chứng thực đầu cuối và tạo khóa, IKE dùng UDP port 500
* ESP (Encapsulation Security Payload) là giao thức cung cấp sự an toàn, toàn vẹn, chứng thực nguồn dữ liệu và một số tùy chọn khác, ESP sử dụng IP protocol number 50
* AH (Authentication Header) là giao thức cung cấp sự toàn vẹn, chứng thực nguồn dữ liệu và một số tùy chọn khác, AH giúp đảm bảo dữ liệu không bị thay đổi trong quá trình truyền dẫn nhưng không mã hóa dự liệu

