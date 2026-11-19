## Lưu ý

### A. Tối ưu băng thông

Load Balancers giữ vai trò trung tâm trong việc duy trì tính khả dụng cao (HA) và độ trễ thấp cho toàn bộ kiến trúc ứng dụng của bạn. Việc tối ưu băng thông giúp Load Balancer xử lý hiệu quả lượng traffic lớn mà không biến nó thành điểm nghẽn.

Để đạt được băng thông tối đa trên các mạng có lưu lượng cao hoặc mạng đường dài độ trễ lớn (Long-Fat Networks - LFN), bạn cần đảm bảo:

1. Phân bổ băng thông phù hợp: Đảm bảo bạn đã đăng ký gói Băng thông đủ lớn để đáp ứng nhu cầu traffic vào các thời điểm cao điểm (xem thêm hướng dẫn tại [Bandwidth](https://docs.greennode.ai/vserver/compute-hcm03-1a/vpc/bandwidth)).

2. Tối ưu hóa OS Kernel & Socket Buffer: Máy chủ client và backend của bạn (hai đầu của luồng traffic) cần được tối ưu hóa ở cấp độ OS kernel để bộ đệm socket không trở thành điểm nghẽn. Hệ thống vLB của GreenNode đã được tối ưu hóa sẵn (pre-tuned) để mang lại băng thông tối đa trong khi vẫn duy trì tính ổn định của kết nối.

    Dưới đây là cấu hình mẫu để tối ưu hóa bộ đệm socket và thuật toán điều khiển tắc nghẽn trên Linux kernel:

    ```bash
    # Tăng dung lượng bộ đệm nhận/gửi tối đa cho socket
    sudo sysctl -w net.core.rmem_max=134217728 
    sudo sysctl -w net.core.wmem_max=134217728 

    # Điều chỉnh bộ nhớ bộ đệm TCP nhận/gửi (tối thiểu - mặc định - tối đa)
    sudo sysctl -w net.ipv4.tcp_rmem="4096 131072 67108864" 
    sudo sysctl -w net.ipv4.tcp_wmem="4096 131072 67108864" 

    # Bật thuật toán điều khiển tắc nghẽn BBR và Fair Queueing
    sudo sysctl -w net.ipv4.tcp_congestion_control=bbr 
    sudo sysctl -w net.core.default_qdisc=fq
    ```

    Để lưu lại các thiết lập này sau khi khởi động lại, hãy thêm các dòng cấu hình trên vào tập tin `/etc/sysctl.conf` và chạy lệnh `sudo sysctl -p`.

> **Trade-offs**: Việc tăng mạnh dung lượng bộ đệm kernel và điều chỉnh thuật toán kiểm soát tắc nghẽn trên các máy chủ đầu cuối sẽ giúp khai thác tối đa dung lượng đường truyền, nhưng đồng thời cũng làm tăng lượng tiêu thụ bộ nhớ (RAM) trên mỗi socket. Chúng tôi khuyên bạn nên giám sát mức sử dụng RAM (`free -m`) và trạng thái socket mạng (`ss -s`) của máy chủ backend khi áp dụng các tham số `sysctl` bộ đệm cao trong môi trường Production.