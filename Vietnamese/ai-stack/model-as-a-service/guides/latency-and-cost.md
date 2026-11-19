---
description: "Phần lớn request chậm hoặc tốn kém là do reasoning, output dài hoặc prompt lặp lại. Các thiết lập dưới đây có tác động lớn nhất."
---

# Tối ưu độ trễ và chi phí

## Nên chỉnh gì

| Yếu tố | Cách làm | Tác dụng |
| --- | --- | --- |
| Reasoning effort | Đặt `minimal` hoặc `low` cho trích xuất, phân loại, câu trả lời ngắn. Mặc định thường là `max`. Xem [Reasoning](../features/reasoning.md). | Ít token output hơn: nhanh và rẻ hơn. |
| Streaming | Đặt `stream: true`. Xem [Streaming](../api-reference/streaming.md). | Người dùng thấy chữ đầu tiên sớm hơn; tổng thời gian không đổi. |
| Prompt caching | Giữ system prompt và tool giống hệt và đặt ở đầu, và chỉ nối thêm vào hội thoại. Xem [Prompt caching](../features/prompt-caching.md). | Input trúng cache rẻ và nhanh hơn. |
| Độ dài output | Yêu cầu câu trả lời ngắn và đặt `max_tokens` có dư cho reasoning. | Token output có giá cao nhất. |
| Chọn model | Dùng model dòng Flash cho việc đơn giản, chỉ dùng flagship khi cần chất lượng. | Giá mỗi token thấp hơn và phản hồi nhanh hơn. |
| Kích thước ngữ cảnh | Chỉ gửi phần lịch sử và tài liệu model cần; rerank trước khi sinh. | Ít token input hơn mỗi request. |

## Đo lường

* `usage` trong mỗi response cho biết token input, output, reasoning và cached.
* `x-kong-upstream-latency` là thời gian chờ model; `x-kong-proxy-latency` là thời gian gateway cộng thêm. Cả hai tính bằng mili giây.
* Trang [Model Usage](https://aiplatform.console.greennode.ai/model-usage) hiển thị token và chi phí theo thời gian.
