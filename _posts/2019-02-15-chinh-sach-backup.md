---
date: 2019-02-15
title: Chính sách backup server trên cloud365
categories:
  - Policy
description: Chính sách backup server trên cloud365
type: Document
---

Hệ thống Cloud của dịch vụ cloud365 của chúng tôi được xây dựng trên nền tảng ảo hóa OpenStack và hệ thống lưu trữ phân tán Ceph. 

<p align="center">
<img src="/images/img-backup/backup.png">
</p>

Nhằm hướng đến một mục đích không downtime đảm bảo hệ thống luôn uptime 99.99%, nhằm đảo bảo dữ liệu của khách hàng luôn được bảo vệ. Chúng tôi luôn quan tâm đến việc nâng cao tính chịu lỗi của hệ thống, từ lựa chọn các công nghệ giải pháp phù hợp đến dự phòng tài nguyên phần cứng, cùng đội ngũ kỹ sư có chuyên môn. Chúng tôi luôn quan tâm đến hoạt động ổn định của hệ thống và. Trên hệ thống lưu trữ phân tán Ceph của chúng tôi luôn luôn tồn tại ít nhất 2 bản ghi của dữ liệu, nhằm đảm bảo việc tài nguyên phần cứng có vấn đề vẫn không ảnh hưởng đến hoạt động của server khách hàng.

Ngoài ra dữ liệu của khách hàng sẽ được backup định kỳ hàng tuần vào mỗi Chủ Nhật qua một hệ thống Server backup khác nhằm đảm bảo dữ liệu của khách hàng vẫn có thể phục hồi sau vì bất cứ một lý do chủ quan hay khách quan không mong muốn nào đó. 

<p align="center">
<img src="/images/img-backup/policybackup.png">
</p>

Chính sách mặc định của dịch vụ Cloud365 là lưu trữ bản backup trong 3 tuần gần nhất, có nghĩa là ngay cả khi xóa 1 server, bản backup sẽ tự động được remove ra khỏi hệ thống sau 3 tuần. Đương nhiên bạn cũng có thể yêu cầu chúng tôi xóa toàn bộ bản backup ngay khi xóa VM. Mọi thay đổi trong chính sách backup chúng tôi sẽ thông báo trên trang chủ một cách công khai cụ thể để khách hàng có thể nắm được. 

Các tính năng để khách hàng có thể chủ động backup và khôi phục dữ liệu đang được thử nghiệm vả sẽ sớm đến tay khách hàng để có thể sử dụng và khai thác trong thời gian sớm nhất.

---
<a href="https://cloud365.vn/" target="_blank">cloud365.vn</a>

Khi cần hỗ trợ xin liên hệ với chúng tôi:

**Công ty phần mềm Nhân Hòa**
- Trụ sở Hà Nội: 32 Võ Văn Dũng, Đống Đa, Hà Nội
- Chi nhánh HCM: 270 Cao Thắng (nối dài), Phường 12,Quận 10, TP HCM
- Hotline: `19006680`