---
description: "OCR xử lý tài liệu — upload file và xử lý bất đồng bộ — nên có bộ endpoint riêng thay vì các endpoint tương thích OpenAI."
---

# OCR API

## Header

| Header | Bắt buộc | Giá trị |
| --- | --- | --- |
| `Authorization` | **Bắt buộc** | `Bearer <API_KEY>` |
| `portal-user-id` | Tùy chọn | Gateway tự gắn theo API key; nếu gửi thì phải trùng user ID trong đường dẫn URL. |

## Gửi tài liệu

**POST** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`

Body là `multipart/form-data`:

| Trường | Bắt buộc | Giá trị nhận | Mô tả |
| --- | --- | --- | --- |
| `flow` | **Bắt buộc** | `single` · `<FLOW_ID>` | `single` chạy OCR cho một tài liệu; flow ID chạy một luồng tài liệu. |
| `doc_type` | Bắt buộc khi `flow=single` | `<DOC_TYPE>` | Loại tài liệu cần trích xuất, ví dụ `Doc2Text` (OCR văn bản chung). Danh sách loại tài liệu khác: liên hệ GreenNode. |
| `file_type` | Bắt buộc khi `flow=single` | `PDF` · `IMAGE` | Loại file upload. |
| `file` | **Bắt buộc** | nhị phân | File cần xử lý. `PDF`: 1 file đuôi `.pdf`, 2 KB–50 MB. `IMAGE`: jpg, jpeg, png, bmp, tif, tiff, mỗi file 2 KB–10 MB, gửi được nhiều file. |

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'flow="single"' \
  --form 'doc_type="<DOC_TYPE>"' \
  --form 'file_type="PDF"' \
  --form 'file=@"<FILE_PATH>"'
```
{% endcode %}

Thành công trả **201** với `data.request_id` (dùng để lấy kết quả) và `data.file_ids` (dùng để tải ảnh kết quả).

## Lấy kết quả

**GET** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```
{% endcode %}

{% hint style="info" %}
**Chưa có dữ liệu?**

Tài liệu đang được xử lý. Chờ 2–5 giây rồi gọi lại (polling) cho tới khi `data.status` = `COMPLETED`. Nếu mãi không có kết quả, gửi `request_id` cho bộ phận hỗ trợ.
{% endhint %}

## Các endpoint kết quả khác

`document_id` lấy từ `data.documents[].document_id` trong response của bước Lấy kết quả.

| Dữ liệu | Method và đường dẫn (sau `…/ocr/ingest`) |
| --- | --- |
| Bảng | `GET /table/<request_id>/<document_id>` |
| Chữ ký | `GET /signature/<request_id>/<document_id>` |
| Con dấu | `GET /stamp/<request_id>/<document_id>` |
| Ảnh kết quả | `GET /file/<request_id>/<file_id>` |

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```
{% endcode %}

## Xử lý lỗi

| Hiện tượng | Nguyên nhân |
| --- | --- |
| `401 Unauthorized` | Thiếu `Authorization` (`missing api key`) hoặc API key sai (`unknown api key`). |
| `403 Forbidden` | User ID trong đường dẫn khác chủ sở hữu API key (`tenant mismatch`). |
| `400 Bad Request` | Thiếu `doc_type` hoặc `file_type` khi `flow=single`, thiếu `file`, hoặc loại / kích thước file không hợp lệ. |
| `404 Not Found` | `request_id` không tồn tại. |
| `500` `Multipart field value cannot be null` | Thiếu trường `flow`. |
| `500` `Doc Type not found` | `doc_type` không tồn tại. |
| Polling không có kết quả | Gửi `request_id`, thời điểm gọi và file mẫu cho bộ phận hỗ trợ. |
