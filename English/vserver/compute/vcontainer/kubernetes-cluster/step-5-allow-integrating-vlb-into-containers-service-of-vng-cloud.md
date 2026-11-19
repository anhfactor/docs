# Step 5: Allow integrating vLB into Containers service of GreenNode

**Demand:**   Customers need to deploy 2 websites: [httpd.app.com](http://httpd.app.com/) and [nginx.app.com](http://nginx.app.com/) according to microservice architecture on GreenNode infrastructure.

**Solution:**   Use vLB (Load Balancer) service in combination with vContainer service on GreenNode.

### **Solution architecture:** <a href="#step5-allowintegratingvlbintocontainersserviceofvngcloud-solutionarchitecture" id="step5-allowintegratingvlbintocontainersserviceofvngcloud-solutionarchitecture"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-5-8_9-39-1.png?version=1&#x26;modificationDate=1684995505000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

***

### **Deployment** <a href="#step5-allowintegratingvlbintocontainersserviceofvngcloud-deployment" id="step5-allowintegratingvlbintocontainersserviceofvngcloud-deployment"></a>

#### **Step 1: Initialize vLB and vContainer** <a href="#step5-allowintegratingvlbintocontainersserviceofvngcloud-step1-initializevlbandvcontainer" id="step5-allowintegratingvlbintocontainersserviceofvngcloud-step1-initializevlbandvcontainer"></a>

1\. Create Network LoadBalancer(Layer 4)

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_13-17-14.png?version=1&#x26;modificationDate=1685693599000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

_Note: Như ở trên, chúng ta sẽ tạo 1 Listener trên Port 80. Nếu muốn sử dụng TLS cho website, có thể tạo thêm Listener trên Port 443 và cấu hình TLS ở LoadBalancer Controller. Bài này sẽ chỉ triển khai với Listener Port 80._\
\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_13-19-49.png?version=1&#x26;modificationDate=1685693600000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_13-21-20.png?version=1&#x26;modificationDate=1685693600000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

2\. Choose **Create Load Balance**r to create vLB

3\. Then access the K8S creation control panel at the link:  [https://hcm-3.console.greennode.ai/vserver/container/cluster](https://hcm-3.console.greennode.ai/vserver/container/cluster):

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-6_16-13-49.png?version=1&#x26;modificationDate=1686042830000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


_Note: When creating vContainer, we can choose Enable LoadBalancer Controller to create cluster with LoadBalancer Controller already deployed. To use the LoadBalancer Controller with the right features according to the needs of the application, in this article, we will not select Enable LoadBalancer Controller but will implement the Nginx LoadBalancer Controller yourself, so you need to disable Ingress Control when initializing K8S._

4\. Check the cluster initialization and download the config file to access the cluster:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-6_16-15-37.png?version=1&#x26;modificationDate=1686042939000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\


<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_13-55-56.png?version=1&#x26;modificationDate=1685693600000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### Step 2: Deploy Nginx LoadBalancer Controller <a href="#step5-allowintegratingvlbintocontainersserviceofvngcloud-step2-deploynginxingresscontroller" id="step5-allowintegratingvlbintocontainersserviceofvngcloud-step2-deploynginxingresscontroller"></a>

1.  Go to [https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters](https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal-clusters)\
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-6_11-29-54.png?version=1&#x26;modificationDate=1686041063000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Copy and run the above command to deploy Nginx LoadBalancer Controller:\
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_14-2-27.png?version=1&#x26;modificationDate=1685693601000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Check:\
    \
    \
    \
    → So we have successfully deployed Nginx LoadBalancer Controller.\
    Service ingress-nginx-controller is initialized with Type: NodePort and listens on Port: 30398, 31873 of Minion Nodes.

    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_14-3-26.png?version=1&#x26;modificationDate=1685693601000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### Step 3: Attach vLB to vContainer <a href="#step5-allowintegratingvlbintocontainersserviceofvngcloud-step3-attachvlbtovcontainer" id="step5-allowintegratingvlbintocontainersserviceofvngcloud-step3-attachvlbtovcontainer"></a>

_Note: By default vLB cannot connect to vContainer Cluster even though it is in the same VPC/Subnet. Therefore, it is necessary to create a new Security Group and attach it to Minion Node._

1.  Create Security Group: Since there is only 1 Listener Port 80 on vLB, only 1 Inbound rule is needed. In case there is a Listener Port 443, please create an Inbound rule.\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-6_15-46-2.png?version=1&#x26;modificationDate=1686041163000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Update Security Group for Minion Node:\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_14-55-40.png?version=1&#x26;modificationDate=1685693601000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  Enter **30398.** Then the Listener will forward traffic to the Backend Pool with port 30398.\
    vLB will periodically health check Pool Members through Monitor Port, traffic will not be sent to members who do not have a successful health check:\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-6_16-16-39.png?version=1&#x26;modificationDate=1686043000000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
4. Click **Save** to finish attaching vLB to vContainer

#### Step 4: Deploy the application <a href="#step5-allowintegratingvlbintocontainersserviceofvngcloud-step4-deploytheapplication" id="step5-allowintegratingvlbintocontainersserviceofvngcloud-step4-deploytheapplication"></a>

1.  Prepare **YAML files**: service.yaml, deployment.yaml and app-ingress.yaml:\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_15-4-58.png?version=1&#x26;modificationDate=1685693602000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Deployment:\
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_15-6-21.png?version=1&#x26;modificationDate=1685693602000&#x26;api=v2" alt=""><figcaption></figcaption></figure>



<figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_15-6-30.png?version=1&#x26;modificationDate=1685693602000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

1.  Check\
    Review the vLB status:\


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_15-8-33.png?version=1&#x26;modificationDate=1685693602000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
2.  Edit hosts file on personal laptop to check: _**C:\Windows\System32\drivers\etc\hosts:**_\
    \
    \
    \


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_15-10-7.png?version=1&#x26;modificationDate=1685693602000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
3.  &#x20;Open a web browser and check:\


    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802513/image2023-6-2_15-11-55.png?version=1&#x26;modificationDate=1685693603000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
