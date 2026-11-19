# MaaS API

**MaaS** provides an **OpenAI-compatible** API for seamless model inference. You can integrate easily using the **Python or JavaScript SDK**, or directly from your **terminal with cURL**.

## 1. OpenAI-compatible API (Chat, Completion, Embedding, Image Generation)

Refer to the scripts under API Usage on the Portal.

_Curl_

<figure><img src="../../.gitbook/assets/image (395).png" alt=""><figcaption></figcaption></figure>

_Python_

<figure><img src="../../.gitbook/assets/image (397).png" alt=""><figcaption></figcaption></figure>

Javascript

<figure><img src="../../.gitbook/assets/image (398).png" alt=""><figcaption></figcaption></figure>

***

## 2. OCR API

OCR is one of the model types available in MaaS. Because it works on documents (file upload, asynchronous processing), it exposes its own set of endpoints instead of the OpenAI-compatible endpoint above. This section explains how to call the OCR API.

### Submit OCR (upload file to create a request)

* **Method**: `POST`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>` (optional — the gateway sets it from the API key; if sent it must match the user ID in the URL)
* **Body**: `multipart/form-data`
  * `flow` (required)
    * `single`: OCR for a single document
    * or `<FLOW_ID>`: OCR for a document workflow (if provided)
  * `doc_type` (required if `flow=single`): `<DOC_TYPE>`, e.g. `Doc2Text` (general text OCR). Contact GreenNode for other document types
  * `file_type` (required if `flow=single`): `PDF` or `IMAGE`
  * `file` (required): file to be processed by OCR. `PDF`: one `.pdf` file, 2 KB–50 MB. `IMAGE`: jpg, jpeg, png, bmp, tif, tiff, 2 KB–10 MB each; multiple files allowed

#### Example

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>' \
  --form 'flow="single"' \
  --form 'doc_type="<DOC_TYPE>"' \
  --form 'file_type="PDF"' \
  --form 'file=@"<FILE_PATH>"'
```

Success returns **201**; the response includes:

* `data.request_id`: used to retrieve results
* `data.file_ids`: used to download result images

### Get OCR Result (use `request_id` to retrieve text/data)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`
* **Headers**:
  * `Authorization: Bearer <API_KEY>`
  * `portal-user-id: <PORTAL_USER_ID>`

#### Example

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### What if no data is returned yet?

This is normal because OCR processing is still in progress.

* Wait 2–5 seconds and call the API again (polling) until `data.status` is `COMPLETED`.
* If the timeout is exceeded and no data is returned, send the `request_id` to the support team for investigation.

### Additional OCR Data APIs (optional, depending on needs)

#### Get Table Data (TABLE)

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### Get Signature Results

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/signature/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

Note: document\_id is `data.documents[].document_id` in the Get OCR Result response.

#### Get Stamp Results

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/stamp/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

#### Download Result Images

* **Method**: `GET`
* **URL**: `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>`

```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/file/<request_id>/<file_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```

### Quick Troubleshooting for OCR

* `401 Unauthorized`:
  * Missing `Authorization` (`missing api key`) or invalid API key (`unknown api key`).
* `403 Forbidden`:
  * The user ID in the path differs from the owner of the API key (`tenant mismatch`).
* `400 Bad Request`:
  * `doc_type` or `file_type` missing when `flow=single`, `file` missing, or an invalid file type / size.
* `404 Not Found`:
  * The `request_id` does not exist.
* `500`:
  * `Multipart field value cannot be null`: the `flow` field is missing.
  * `Doc Type not found`: the `doc_type` does not exist.
* Polling does not return results:
  * Provide `request_id` + timestamp + sample file (if possible) to the support team for further investigation.
