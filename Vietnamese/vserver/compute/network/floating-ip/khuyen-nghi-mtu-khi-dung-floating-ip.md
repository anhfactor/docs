---
description: Giữ MTU <= 4000 khi dùng Floating IP cho outbound Internet.
---

# Khuyến nghị MTU khi dùng Floating IP

Khi sử dụng **Floating IP** để truy cập Internet theo chiều **outbound**, hãy cấu hình MTU gói tin **<= 4000** để giảm rủi ro **mất gói (packet loss)**.

{% hint style="warning" %}
Nếu MTU quá lớn, đường truyền có thể bị phân mảnh hoặc rơi gói. Điều này thường gây lỗi khó đoán trong TCP/TLS.
{% endhint %}

Xem thêm: [MTU và “DF flag” best practice on GreenNode](../../../vmarketplace/network-software-installation/pfsense-tren-hcm03/mtu-va-df-flag-best-practice-on-vng-cloud.md)
