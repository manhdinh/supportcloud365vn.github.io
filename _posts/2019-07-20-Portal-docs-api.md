---
date: 2019-07-20
title: Tài liệu API của portal
categories:
  - Tài liệu API
description: Tài liệu API dành cho User của portal cloud365
type: Document
---

# Docs API portal dành cho User.

## 1. API xác thực
### 1. Tạo mới Token.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/auth/tokens
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| email(*) | Body | Email | Email đăng nhập vào portal |
| password(*) | Body | String | Mật khẩu đăng nhập vào portal của tài khoản muốn lấy token |
| expired | Body | Integer | Nhập số giờ tồn tại của Token |
| project_id | Body | String | Nếu như tài khoản có nhiều hơn một project cần nhập project để chỉ định project thao tác |

- Request mẫu:

```sh
{
    "email": "string",
    "password": "string",
    "expired": 0,
    "project_id": "string"
}
```

- Respone mẫu:

```sh
{
    "message": "Xác thực thành công",
    "token": "string"
}
```

### 2. Lấy thông tin chi tiết Token.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/auth/tokens
- Respone mẫu:

```sh
{
    "project_id": "string",
    "token_created": "YYYY-MM-DDTh:i:s+07:00",
    "token_expired": "YYYY-MM-DDTh:i:s+07:00",
    "token_key": "string",
    "user_owner": "user@example.com"
}
```

### 3. Xóa Token.

- Phương thức: DEL
- Đường dẫn: http://portalurl/api/v1/auth/tokens

## 2. API phục vụ cho thao tác và điều khiển máy chủ ảo.

### 1. Liệt kê các máy chủ ảo đang sở hữu.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/server/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| page | Query | Integer | Nhập trang muốn xem |
| page_size | Query | Integer | Số lượng phần tử hiển thị tối đa trên một trang |
| server_id | Query | String | Tìm theo server ID |
| server_ip | Query | String | Tìm theo địa chỉ IP |
| server_name | Query | String | Tìm theo tên máy chủ ảo|
| server_status | Query | String | Tìm theo trạng thái của máy chủ ảo |
| server_expired | Query | String | Tìm theo thời gian hết hạn của máy chủ ảo |
| server_created | Query | String | Tìm theo thời gian khởi tạo của máy chủ ảo |

- Respone mẫu:

```sh
{
  "count": 0,
  "next": "http://example.com",
  "previous": "http://example.com",
  "results": [
    {
      "instance_id": "string",
      "status": "string",
      "addresses": "string",
      "name": "string",
      "created": "2019-07-18T06:41:10Z",
      "expired": "2019-07-18T06:41:10Z",
      "ip_addresses": [
        "string"
      ],
      "region": "string"
    }
  ]
}
```

### 2. Thông tin chi tiết máy chủ ảo.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn xem thông tin chi tiết |

- Respone mẫu:

```sh
{
  "instance_id": "string",
  "status": "string",
  "addresses": "string",
  "name": "string",
  "created": "2019-07-18T06:41:10Z",
  "expired": "2019-07-18T06:41:10Z",
  "ip_addresses": [
    "string"
  ],
  "region": "string"
}
```

### 3. Thay đổi mật khẩu máy chủ ảo.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/change_password/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn thay đổi mật khẩu|
| password(*) | Body | String | Mật khẩu muốn thay đổi |
| re_password(*) | Body | String | Nhập lại mật khẩu muốn thay đổi |

- Request mẫu:

```sh
{
  "password": "string",
  "re_password": "string"
}
```

- Respone mẫu:

```sh
{
  "message": "string"
}
```

### 4. lấy đường dẫn console của server.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/console/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn lấy thông tin đường dẫn console|

- Respone mẫu:

```sh
[
  {
    "message": "string",
    "url": "example.com"
  }
]
```

### 5. Lấy thông tin nhật ký boot của máy chủ ảo.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/get_console_log/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn lấy thông tin console log |

- Respone mẫu:

```sh
{
  "console_log": "string"
}
```

### 6. Lấy thông tin các volume gắn vào máy chủ ảo.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/list_volume_attached/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn lấy thông tin các volume gắn vào |

- Respone mẫu:

```sh
[
  {
    "bootable": "true",
    "name": "string",
    "size": 0,
    "volume_id": "string"
  },
  {}
]
```

### 7. Khởi động lại máy chủ ảo.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/reboot/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn khởi động lại |

- Respone mẫu:

```sh
{
  "message": "string"
}
```

### 8. Khởi động máy chủ ảo.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/start/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn khởi động |

- Respone mẫu:

```sh
{
  "message": "string"
}
```

### 9. Tắt máy chủ ảo.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/stop/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn tắt |

- Respone mẫu:

```sh
{
  "message": "string"
}
```

### 10. Đổi tên máy chủ ảo.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/rename/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn đổi tên |
| server_name(*) | Body | String | Tên máy chủ ảo muốn thay đổi |

- Request mẫu:

```sh
{
  "server_name": "string"
}
```

- Respone mẫu:

```sh
{
  "message": "string"
}
```

### 11. Rebuild máy ảo => Thay đổi hệ điều hành của máy chủ ảo.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/server/{instance_id}/rebuild/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| instance_id(*) | Path | String | server_id của máy chủ ảo muốn đổi tên |
| os_image(*) | Body | Integer | ID của hệ điều hành muốn thay đổi |

- Request mẫu:

```sh
{
  "os_image": 0
}
```

- Respone mẫu:

```sh
{
  "message": "string"
}
```

## 3. API phục vụ cho việc quản lý thông tin cá nhân của User.

### 1. Lấy thông tin cá nhân.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/user/detail_user/
- Respone mẫu:

```sh
{
    "address": "string",
    "birthday": "YYYY-MM-DD",
    "company": "string",
    "date_joined": "YYYY-MM-DDTh:i:s+07:00",
    "email": "user@example.com",
    "first_name": "string",
    "gender": "gender",
    "last_login": "YYYY-MM-DDTh:i:s+07:00",
    "last_name": "string",
    "phone_number": "00000000"
}
```

### 2. Cập nhật, thay đổi thông tin cá nhân.

- Phương thức: PATCH
- Đường dẫn: http://portalurl/api/v1/user/update_profile/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| first_name | Body | String | Họ và tên đệm |
| last_name | Body | String | Tên thật |
| gender | Body | Integer | Giới tính, 1 => Nam, 2 => Nữ , 3 => Công ty |
| phone_number | Body | String | Số điện thoại của người sở hữu |
| address | Body | String | Địa chỉ |
| company | Body | String | Tên công ty |

- Request mẫu:

```sh
{
    "first_name": "string",
    "last_name": "string",
    "gender": 0,
    "phone_number": "string",
    "address": "string",
    "company": "string"
}
```

- Respone mẫu:

```sh
{
    "message": "string"
}
```

### 3. Thay đổi mật khẩu của người dùng.

- Phương thức: POST
- Đường dẫn: http://portalurl/api/v1/user/change_password/
- Tham số:

| Tên biến | Vị trí | Kiểu dữ liệu | Mô tả |
|----------|--------|--------------|-------|
| old_password(*) | Body | String | Mật khẩu cũ của tài khoản |
| new_password(*) | Body | String | Mật khẩu mới muốn thay đổi |
| re_password(*) | Body | String | Nhập lại mật khẩu mới muốn thay đổi|

- Request mẫu:

```sh
{
    "old_password": "string",
    "new_password": "string",
    "re_password": "string"
}
```

- Respone mẫu:

```sh
{
    "message": "string"
}
```

### 4. Liệt kê các project mà tài khoản sở hữu.

- Phương thức: GET
- Đường dẫn: http://portalurl/api/v1/user/list_project/
- Respone mẫu:

```sh
{
    "is_available": true,
    "project": "string",
    "project_user_name": "string"
}
```

---
<a href="https://cloud365.vn/" target="_blank">cloud365.vn</a>

Khi cần hỗ trợ xin liên hệ với chúng tôi:

**Công ty phần mềm Nhân Hòa**
- Trụ sở Hà Nội: 32 Võ Văn Dũng, Đống Đa, Hà Nội
- Chi nhánh HCM: 270 Cao Thắng (nối dài), Phường 12,Quận 10, TP HCM
- Hotline: `19006680`
