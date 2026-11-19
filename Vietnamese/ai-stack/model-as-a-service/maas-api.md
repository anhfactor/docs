# MaaS API

**MaaS** cung cấp một API **tương thích với OpenAI** để thực hiện suy luận mô hình một cách liền mạch. Bạn có thể dễ dàng tích hợp bằng **Python, JavaScript SDK**, hoặc trực tiếp qua **terminal với cURL**.

## 1. API tương thích OpenAI (Chat, Completion, Embedding, Image Generation)

Tham khảo các Script trong API Usage trên Portal

_Curl_

<figure><img src="../../.gitbook/assets/image (26) (2).png" alt=""><figcaption></figcaption></figure>

_Python_

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Javascript

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (2) (1).png" alt=""><figcaption></figcaption></figure>

***

## 2. OCR API

OCR là một loại model trong MaaS, nhưng do đặc thù xử lý tài liệu (upload file, xử lý bất đồng bộ) nên có bộ endpoint riêng thay vì dùng endpoint tương thích OpenAI ở trên. Phần dưới đây hướng dẫn cách gọi OCR API.

### Submit OCR (upload file để tạo request)

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>` (tùy chọn — gateway tự gắn theo API key; nếu gửi phải trùng user ID trong URL)
* **Body**: `multipart/form-data`
  * `flow` (required)
    * `single`: OCR 1 tài liệu
    * hoặc `<FLOW_ID>`: OCR theo bộ tài liệu (nếu bạn được cấp flow)
  * `doc_type` (required nếu `flow=single`): `<DOC_TYPE>`, ví dụ `Doc2Text` (OCR văn bản chung). Loại tài liệu khác: liên hệ GreenNode
  * `file_type` (required nếu `flow=single`): `PDF` hoặc `IMAGE`
  * `file` (required): file cần OCR. `PDF`: 1 file đuôi `.pdf`, 2 KB–50 MB. `IMAGE`: jpg, jpeg, png, bmp, tif, tiff, mỗi file 2 KB–10 MB, gửi được nhiều file

#### Ví dụ

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'flow="single"' \
  --form 'doc_type="<DOC_TYPE>"' \
  --form 'file_type="PDF"' \
  --form 'file=@"<FILE_PATH>"'
```

Thành công trả **201**, response chứa:

* `data.request_id`: dùng để lấy kết quả
* `data.file_ids`: dùng để tải ảnh kết quả

### Get OCR Result (dùng `request_id` để lấy text/data)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>`

#### Ví dụ

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### Nếu gọi ra chưa thấy data?

Điều này bình thường vì OCR đang xử lý.

* Đợi 2–5 giây và gọi lại API này (polling) cho tới khi `data.status` = `COMPLETED`.
* Nếu quá thời gian timeout mà vẫn không có dữ liệu, gửi `request_id` cho team support để kiểm tra.

### Các API lấy thêm dữ liệu khác của OCR (tuỳ nhu cầu)

#### Lấy bảng (TABLE)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### Lấy kết quả chữ ký

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

Note: document\_id nằm trong `data.documents[].document_id` của response Get OCR Result

#### Lấy kết quả con dấu

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### Tải ảnh kết quả

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

### Troubleshooting nhanh cho OCR

* `401 Unauthorized`:
  * Thiếu `Authorization` (`missing api key`) hoặc API key sai (`unknown api key`).
* `403 Forbidden`:
  * User ID trong đường dẫn khác chủ sở hữu API key (`tenant mismatch`).
* `400 Bad Request`:
  * Thiếu `doc_type` hoặc `file_type` khi `flow=single`, thiếu `file`, hoặc loại / kích thước file không hợp lệ.
* `404 Not Found`:
  * `request_id` không tồn tại.
* `500`:
  * `Multipart field value cannot be null`: thiếu trường `flow`.
  * `Doc Type not found`: `doc_type` không tồn tại.
* Polling mãi chưa ra kết quả:
  * Gửi `request_id` + thời điểm gọi + file mẫu (nếu được) cho team support.
