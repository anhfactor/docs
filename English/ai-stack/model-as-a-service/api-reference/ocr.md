---
description: "OCR works on documents — file upload and asynchronous processing — so it has its own endpoints instead of the OpenAI-compatible ones."
---

# OCR API

## Headers

| Header | Required | Value |
| --- | --- | --- |
| `Authorization` | **Required** | `Bearer <API_KEY>` |
| `portal-user-id` | Optional | The gateway sets it from the API key; if you send it, it must match the user ID in the URL path. |

## Submit a document

**POST** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest`

The body is `multipart/form-data`:

| Field | Required | Accepted values | Description |
| --- | --- | --- | --- |
| `flow` | **Required** | `single` · `<FLOW_ID>` | `single` runs OCR on one document; a flow ID runs a document workflow. |
| `doc_type` | Required when `flow=single` | `<DOC_TYPE>` | The document type to extract, e.g. `Doc2Text` (general text OCR). Contact GreenNode for other document types. |
| `file_type` | Required when `flow=single` | `PDF` · `IMAGE` | Type of the uploaded file. |
| `file` | **Required** | binary | The file to process. `PDF`: one `.pdf` file, 2 KB–50 MB. `IMAGE`: jpg, jpeg, png, bmp, tif, tiff, 2 KB–10 MB each; multiple files allowed. |

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

Success returns **201** with `data.request_id` (used to fetch results) and `data.file_ids` (used to download result images).

## Get the result

**GET** `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>`

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/<request_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```
{% endcode %}

{% hint style="info" %}
**No data yet?**

Processing is still running. Wait 2–5 seconds and call again (polling) until `data.status` is `COMPLETED`. If it never returns, send the `request_id` to support.
{% endhint %}

## More result endpoints

`document_id` comes from `data.documents[].document_id` in the Get result response.

| Data | Method and path (after `…/ocr/ingest`) |
| --- | --- |
| Tables | `GET /table/<request_id>/<document_id>` |
| Signatures | `GET /signature/<request_id>/<document_id>` |
| Stamps | `GET /stamp/<request_id>/<document_id>` |
| Result images | `GET /file/<request_id>/<file_id>` |

{% code title="curl" %}
```bash
curl --location 'https://maas-llm-aiplatform-hcm.api.vngcloud.vn/maas/user-<PORTAL_USER_ID>/greennode/idp/v1/ocr/ingest/table/<request_id>/<document_id>' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'portal-user-id: <PORTAL_USER_ID>'
```
{% endcode %}

## Troubleshooting

| Symptom | Cause |
| --- | --- |
| `401 Unauthorized` | Missing `Authorization` (`missing api key`) or invalid API key (`unknown api key`). |
| `403 Forbidden` | The user ID in the path differs from the owner of the API key (`tenant mismatch`). |
| `400 Bad Request` | `doc_type` or `file_type` missing when `flow=single`, `file` missing, or an invalid file type / size. |
| `404 Not Found` | The `request_id` does not exist. |
| `500` `Multipart field value cannot be null` | The `flow` field is missing. |
| `500` `Doc Type not found` | The `doc_type` does not exist. |
| Polling never returns | Send `request_id`, the time of the call and a sample file to support. |
