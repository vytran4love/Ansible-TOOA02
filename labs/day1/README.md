##  CÀI ĐẶT MÔI TRƯỜNG

#### Yêu cầu:
- Cài đặt ansible
- Cài đặt ssh connection theo yêu cầu
  Host server: 192.168.33.10
  Client server: 192.168.33.12
Host server sẽ kết nối SSH tới client server bằng file key.

## INVENTORY

#### Yêu cầu:
Viết file inventory theo cấu trúc ini:
- Web ( ip 10.0.0.71, 10.0.1.71, 10.0.2.71, 10.0.2.71)
- Api ( ip 10.0.0.72, 10.0.1.72, 10.0.2.72, 10.0.2.72)
- Environment nightly: 10.0.0.71, 10.0.0.72 => using ssh\_key: dev.pem
- Environment staging: 10.0.1.71, 10.0.1.72 => using ssh\_key: staging.pem
- Environment prod: 10.0.2.71, 10.0.2.72 => using ssh\_key: prod.pem
- user\_ssh: ubuntu

Sử dụng ansible-inventory để list group các hosts

