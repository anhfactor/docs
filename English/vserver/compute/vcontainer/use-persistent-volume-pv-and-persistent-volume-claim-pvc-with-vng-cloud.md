# Use Persistent Volume (PV) and Persistent Volume Claim (PVC) with GreenNode

PersistentVolume(PV) is a part of the data storage space in the cluster, the PersistentVolume is the same as the normal Volume, but it exists independently of the POD (the pod deleted PV still exists), there are many types of PersistentVolume that can be deployed. like NFS, Clusterfs...

PersistentVolumeClaim(PVC) is required to use storage space (use PV). Visualize PV as Node, PVC as POD. POD running will use NODE's resources, PVC operation it uses PV's resources.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-12-34.png?version=1&#x26;modificationDate=1684996043000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Step 1: Create PersistentVolume(PV) and PersistentVolumeClaim(PVC)** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-step1-createpersistentvolume-pv-and" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-step1-createpersistentvolume-pv-and"></a>

#### **1. Prepare yaml file to create PV and PVC** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-1.prepareyamlfiletocreatepvandpvc" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-1.prepareyamlfiletocreatepvandpvc"></a>

`nginx-pvc.yaml`

\---

apiVersion: v1

kind: PersistentVolumeClaim

metadata:

name: nginx-pvc

spec:

&#x20;    accessModes:

&#x20;    \- ReadWriteOnce

&#x20;    resources:

requests:

&#x20;   storage: 2Gold

#### **2. Create PV and PVC** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-2.createpvandpvc" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-2.createpvandpvc"></a>

\# kubectl apply -f nginx-pvc.yaml

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-34-33.png?version=1&#x26;modificationDate=1684996343000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-35-23.png?version=1&#x26;modificationDate=1684996343000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

At this time, PV will automatically be created and will belong to StorageClass: csi-sc-cinderplugin-ssd because GreenNode is already defined with information of volume: SSD-IOPS-3000

#### **3. Check on GreenNode portal** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-3.checkonvngcloudportal" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-3.checkonvngcloudportal"></a>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-24-47.png?version=1&#x26;modificationDate=1684996553000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Step 2: Use PersistentVolumeClaim** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-step2-usepersistentvolumeclaim" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-step2-usepersistentvolumeclaim"></a>

#### **1. Prepare yaml file to use PVC:** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-1.prepareyamlfiletousepvc" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-1.prepareyamlfiletousepvc"></a>

web-deployment.yaml

\---

| `apiVersion:` `apps/v1 kind:` `Deployment metadata:` `name:` `web-deployment spec:` `replicas:` `1   selector:` `matchLabels:` `app:` `nginx   template:` `metadata:` `labels:` `app:` `nginx     spec:` `volumes:` `- name:` `nginx-volume         persistentVolumeClaim:` `claimName:` `nginx-pv           readOnly:` `false` `containers:` `- image:` `nginx         imagePullPolicy:` `IfNotPresent         name:` `web-app         ports:` `- containerPort:` `80           protocol:` `TCP         volumeMounts:` `- mountPath:` `/usr/share/nginx/html           name:` `nginx-volume`  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### **2. Application Deployment** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-2.applicationdeployment" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-2.applicationdeployment"></a>

\# kubectl  apply  -f  web-deployment.yaml

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-37-26.png?version=1&#x26;modificationDate=1684997603000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-37-15.png?version=1&#x26;modificationDate=1684997663000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**3. Check:**

Access the container and create the file:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-38-11.png?version=1&#x26;modificationDate=1684997693000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
\# kubectl exec -it  web-deployment-859679cc57-v8kw4 bash

**4. Delete deployment**

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-27-42.png?version=1&#x26;modificationDate=1684997873000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\# kubectl delete -f web-deployment.yaml

**5. Re-create deployment: this time the system will create new Pods, Containers**\
\# kubectl apply  -f web-deployment.yaml

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-28-47.png?version=1&#x26;modificationDate=1684997903000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**6. Access to the new container to check if the data on the PersistentVolume is lost**\
\# kubectl exec -it  web-deployment-859679cc57-tglfg  bash

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-39-46.png?version=1&#x26;modificationDate=1684997963000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\=> As can be seen here, the data on the Persistent Volume is not lost.

### **Step 3: Remove PersistentVolume and PersistentVolumeClaim** <a href="#usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-step3-removepersistentvolumeandpers" id="usepersistentvolume-pv-andpersistentvolumeclaim-pvc-withvngcloud-step3-removepersistentvolumeandpers"></a>

When no longer need to use, customers can delete PV (Note need to delete resources that are using PVC before deleting PV):\
\# kubectl delete -f nginx-pvc.yaml

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802536/image2023-4-26_13-40-4.png?version=1&#x26;modificationDate=1684998379000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
