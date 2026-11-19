# Object storage (HCM03)

{% hint style="warning" %}
The HCM03 farm no longer accepts new customers. Existing customers can continue to use the service. New customers should use the [HCM04](../object-storage-hcm04/) or [HAN02](../object-storage-han02/) farm.
{% endhint %}

**Object Storage** (also known as **Object Storage**, **Cloud Storage**) is a form of data storage in discrete units called **objects**. Each object contains the actual data (such as images, videos, files) along with metadata that provides information about the object.

**Benefits of Object Storage:**

* **High durability and availability** due to backup and redundancy features.
* **Rich metadata**: Enhanced data management and retrieval capabilities.
* **Scalability**: Easily expandable without complex reconfiguration or downtime.
* **Cost efficiency**: Often provides lower costs compared to traditional storage solutions, especially for large data storage needs.

***

## **Farm** <a href="#farm" id="farm"></a>

Farm is a term specifically used for vStorage. A farm is defined by us as a system that includes infrastructure, services, etc., deployed at a specific location in two regions, Hanoi and Ho Chi Minh City, with the purpose of providing vStorage storage services. For the two farms HCM03 and HAN01, we provide the specific parameters for each farm as follows:

<table data-full-width="true"><thead><tr><th>Farm</th><th>Farm ID</th><th>Authentication endpoint</th><th>vStorage endpoint</th><th>Purpose of use</th></tr></thead><tbody><tr><td>HCM03</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</td><td>https://hcm03.auth.vstorage.vngcloud.vn/v3</td><td>https://hcm03.vstorage.vngcloud.vn</td><td>The farm serves multiple purposes and is shared for the project's initial data in the HoChiMinh Region.</td></tr><tr><td>HCM03</td><td>8b1e9c9b-7123-54a5-ua8f-2d67d71c9212</td><td>https://hcm03.auth.vstorage.vngcloud.vn/v3</td><td>https://hcm03-encrypt-vstorage.vngcloud.vn</td><td>When using this encryption endpoint, your data will be automatically encrypted when uploading files to vStorage in accordance with the AES-256 encryption standard.</td></tr></tbody></table>

{% include "../../../.gitbook/includes/private-endpoint-acl-requirement.md" %}

To find specific information please refer [here](../what-is-vstorage/what-is-farm.md).

***

## Resource Quota <a href="#han-muc-tai-nguyen" id="han-muc-tai-nguyen"></a>

Các bảng sau đây liệt kê các giá trị tối đa cho tài nguyên lưu trữ trên vStorage của bạn.

### Bandwidth <a href="#bandwidth" id="bandwidth"></a>

<table data-full-width="true"><thead><tr><th>Farm</th><th>Download BW Domestic</th><th>Download BW International</th><th>Upload BW Domestic</th><th>Upload BW International</th></tr></thead><tbody><tr><td>HCM03</td><td>10Gbps shared</td><td>300Mbps</td><td>10Gbps shared</td><td>300Mbps</td></tr></tbody></table>

### Request per limit <a href="#request-per-limit" id="request-per-limit"></a>

* Per IP

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Request all types</th><th>Put request</th><th>Get request</th></tr></thead><tbody><tr><td>Gold</td><td>2500 request/s/IP</td><td>1000 request/s/IP</td><td>1500 request/s/IP</td></tr></tbody></table>

* Per path

<table data-full-width="true"><thead><tr><th>Storage Class</th><th>Request all types</th><th>Put request</th><th>Get request</th></tr></thead><tbody><tr><td>Gold</td><td>2500 request/s/path</td><td>1000 request/s/path</td><td>1500 request/s/path</td></tr></tbody></table>

### Others <a href="#cac-han-muc-khac" id="cac-han-muc-khac"></a>

<table data-full-width="true"><thead><tr><th>Item</th><th>Limit</th></tr></thead><tbody><tr><td>Number of object per container/bucket</td><td>600 millions</td></tr><tr><td>Number of container/ bucker per project</td><td>Unlimited</td></tr></tbody></table>
