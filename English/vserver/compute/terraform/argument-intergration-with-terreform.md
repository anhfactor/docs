# Argument Intergration with Terraform

{% hint style="info" %}
**Content**

* [Arguments tranfer from Terraform](argument-intergration-with-terreform.md#argumentintergrationwithterreform-argumentstranferfromterreform)
* [Attributes transfer to Terraform](argument-intergration-with-terreform.md#argumentintergrationwithterreform-attributestransfertoterreform)
{% endhint %}

## **Arguments transfer from Terraform** <a href="#argumentintergrationwithterreform-argumentstranferfromterreform" id="argumentintergrationwithterreform-argumentstranferfromterreform"></a>

***

### Example Usage <a href="#argumentintergrationwithterreform-exampleusage" id="argumentintergrationwithterreform-exampleusage"></a>

```
resource "vngcloud_vserver_server" "server"{
 project_id = "pro-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
 name = "example-server"
 encryption_volume = false
 flavor_id = "flav-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
 image_id = "img-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
 network_id = "net-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
 root_disk_size = 20
 root_disk_type_id = "vtype-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
 ssh_key = "ssh-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
 security_group = ["secg-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"]
 subnet_id = "sub-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```

### Arguments Reference <a href="#argumentintergrationwithterreform-argumentsreference" id="argumentintergrationwithterreform-argumentsreference"></a>

<table data-full-width="true"><thead><tr><th width="74">No.</th><th width="175">Arguments</th><th width="118">Required</th><th width="117">Data Type</th><th width="131">Description</th><th>Example Data</th></tr></thead><tbody><tr><td>1</td><td><em>project_id</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>ID of the Project.</td><td>pro-462803f3-6858-466f-bf05-df2b33faa360</td></tr><tr><td>2</td><td><em>name</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>Name of Server.</td><td>example-server-name</td></tr><tr><td>3</td><td><em>encryption_volume</em></td><td><strong>REQUIRED</strong></td><td><strong>BOOLEAN</strong></td><td>Is Server use encryption volume?</td><td>False</td></tr><tr><td>4</td><td><em>flavor_id</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>ID of the Flavor.</td><td>flav-e2028a81-cc75-47e4-8af1-9eef2f857f84</td></tr><tr><td>5</td><td><em>image_id</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>ID of the Image.</td><td>img-b5bf635e-0456-4765-b493-31d5fcfc05aa</td></tr><tr><td>6</td><td><em>network_id</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>ID of Network.</td><td>net-961d6867-b65a-40ac-879e-d84e4dc768e0</td></tr><tr><td>7</td><td><em>root_disk_size</em></td><td><strong>REQUIRED</strong></td><td><strong>NUMBER</strong></td><td>Size of boot volume.</td><td>20</td></tr><tr><td>8</td><td><em>root_disk_type_id</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>ID of boot volume type.</td><td>vtype-61c3fc5b-f4e9-45b4-8957-8aa7b6029018</td></tr><tr><td>9</td><td><em>ssh_key</em></td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>ID of SSH key.</td><td>ssh-7bd70c56-1f05-4989-a0f0-cc3496b62001</td></tr><tr><td>10</td><td><em>security_group</em></td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>ID of Security Group.</td><td>secg-3b12a078-b862-43b5-a56b-d7fc4429e535</td></tr><tr><td>11</td><td><em>subnet_id</em></td><td><strong>REQUIRED</strong></td><td><strong>STRING</strong></td><td>ID of the subnet.</td><td>sub-c1ebba8f-baa8-434c-beb7-2916199bb812</td></tr><tr><td>12</td><td>host_group_id</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>ID of Host Group.</td><td>/</td></tr><tr><td>13</td><td>action</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>Action with Server. It can be: stop, start; reboot.</td><td>start</td></tr><tr><td>14</td><td>attach_floating</td><td><strong>OPTIONAL</strong></td><td><strong>BOOLEAN</strong></td><td>Is Server attach a floating IP?</td><td>True</td></tr><tr><td>15</td><td>expire_password</td><td><strong>OPTIONAL</strong></td><td><strong>BOOLEAN</strong></td><td>Skip change password: false, else: true.</td><td>False</td></tr><tr><td>16</td><td>os_licence</td><td><strong>OPTIONAL</strong></td><td><strong>BOOLEAN</strong></td><td>License of OS.</td><td>True</td></tr><tr><td>17</td><td>root_disk_encryption_type</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>Type encryption of boot volume.</td><td>/</td></tr><tr><td>18</td><td>source_type</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>Type of Source.</td><td>/</td></tr><tr><td>19</td><td>user_name</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>Name of User.</td><td>usernamestackops</td></tr><tr><td>20</td><td>user_password</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>Password of User.</td><td>VngGCloud3030</td></tr><tr><td>21</td><td>server_group</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>ID của Server Group.</td><td>/</td></tr><tr><td>22</td><td>user_data</td><td><strong>OPTIONAL</strong></td><td><strong>STRING</strong></td><td>User_data to provide when launching the server.</td><td>${data.template_cloudinit_config.user_data.rendered}</td></tr><tr><td>23</td><td>user_data_base64_encode</td><td><strong>OPTIONAL</strong></td><td><strong>BOOLEAN</strong></td><td>Can be used instead of user_data to pass base64-encoded binary data directly. Use this instead of user_data whenever the value is not a valid UTF-8 string.</td><td>True</td></tr><tr><td>24</td><td>is_poc</td><td><strong>OPTIONAL</strong></td><td><strong>BOOLEAN</strong></td><td>using POC wallet</td><td>True</td></tr></tbody></table>

{% hint style="warning" %}
**Note**

* With any changed argument (resize), still tranfering argument is\_poc to GreenNode.
* If it does not tranfer is\_poc, user going to using credit wallet.
* If the POC wallet is discontinued and subsequently the server expires, the server does not shut down immediately. Instead, the VNG system has a scheduled job that scans (at 11 AM daily) to consider shutting down expired servers. Therefore, before 11 AM, users can top up credit to continue using the server.
{% endhint %}

{% hint style="info" %}
**Important**

When a resource is expired and status be Terminated, if User would like to renew a resource, **User must to implement Renew in User Portal when using Terraform**, due to Terraform does not have the ability to renew.
{% endhint %}

## Attributes transfer to Terraform <a href="#argumentintergrationwithterreform-attributestransfertoterreform" id="argumentintergrationwithterreform-attributestransfertoterreform"></a>

***

When GreenNode System has recorded all arguments above from Terraform, the following attributes are exported:

* **id** STRING : ID of this Server
* **external\_interfaces:** (List of Map of String) List of Network external interface. It included:
  * **external\_interfaces** STRING;
  * **floating\_ip** STRING;
  * **interface\_type**STRING;
  * **mac** STRING;
  * **network\_uuid** STRING;
  * **port\_uuid** STRING;
  * **status** STRING;
  * **subnet\_uuid** STRING;
  * **type** STRING;
* **internal\_interfaces:** (List of Map of String) List of Network external interface. It included:
  * **external\_interfaces** STRING;
  * **floating\_ip** STRING;
  * **interface\_type** STRING;
  * **mac** STRING;
  * **network\_uuid** STRING;
  * **port\_uuid** STRING;
  * **status** STRING;
  * **subnet\_uuid** STRING;
  * **type** STRING./.
