# Step 4: Deploy Application on Initialized Container

**Step 1**: initialize the Deployment file - in this case, use the YANL . file

1.myapp-deploy.yaml

apiVersion: apps/v1\
kind: Deployment\
metadata:

\# name of deployment\
name: deployapp

spec:

\# number of PODs generated\
replicas: 3

\# set up deploy-managed PODs, which are PODs labeled "app=deployapp"\
selector:\
&#x20;   matchLabels:\
&#x20;       app: deployapp

\# Define POD template, when needed Deploy uses this template to create Pod

**template:**\
&#x20;   metadata:\
&#x20;       name: podapp\
&#x20;       labels:\
&#x20;           app: deployapp\
spec:\
&#x20;  containers:\
&#x20;      name: node\
&#x20;      image: ichte/swarmtest:node\
&#x20;      resources:\
&#x20;          limits:\
&#x20;             memory: "128Mi"\
&#x20;             cpu: "100m"\
&#x20;      ports:\
&#x20;             containerPort: 8085

Execute the following command to deploy:

`kubectl apply -f 1.myapp-deploy.yaml`\
\
When the Deployment is created, its name is deployapp, which can be checked with the command:

`kubectl get deploy -o wide`\
\
This deploy creates a ReplicasSet and manages it, type the following command to display the ReplicaSet

`kubectl get rs -o wide`\
In turn, the Deploy-managed ReplicaSet manages (creates, deletes) the Pods, to view the Pods.

`kubeclt get po -o wide`

\# Or filter the whole label\
`kubectl get po -l "app=deployapp" -o wide`

*   Example: Case deploy APP echo1:\
    \
    \
    <br>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802500/Screen%20Shot%202021-05-24%20at%2010.45.23.png?version=1&#x26;modificationDate=1684985050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
*   Check the deployment:\
    \
    \
    <br>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/59802500/Screen%20Shot%202021-05-24%20at%2010.49.56.png?version=1&#x26;modificationDate=1684985050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 2:** Expose Services Just deployed to Public\
\
\
Thực hiện apply cấu hinh len Container:\
\
\
Test access from outside the Internet to Echo1 Service with port 30309

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802500/Screen%20Shot%202021-05-24%20at%2010.53.14.png?version=1&#x26;modificationDate=1684985050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802500/Screen%20Shot%202021-05-24%20at%2010.57.50.png?version=1&#x26;modificationDate=1684985050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

\
\
\
That's it, I've finished the application and Expose to the internet

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802500/Screen%20Shot%202021-05-24%20at%2010.58.05.png?version=1&#x26;modificationDate=1684985050000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

<br>
