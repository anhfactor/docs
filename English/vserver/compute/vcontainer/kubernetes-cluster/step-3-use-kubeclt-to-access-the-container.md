# Step 3: Use Kubeclt to access the Container

**Step 1:** Note that you need to initialize at SSH KEY to be able to access all Master, Minion

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802494/image2023-6-2_10-36-30.png?version=1&#x26;modificationDate=1685676991000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 2:** Download the Config Container file on the GreenNode portal

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802494/image2023-6-2_10-34-21.png?version=1&#x26;modificationDate=1685676862000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 3:** Copy the Configure file into the Kubectl configuration file on PC/Laptop&#x20;

Kubectl on MAC OS

Step 3.1: cd \~/

Step 3.2: mkdir .kube

Step 3.3: cd .kube

Step 3.4: vim config

Step 3.5: Copy the Config File on the Portal downloaded into the config file on MAC OS:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802494/Screen%20Shot%202021-05-24%20at%2010.34.41.png?version=1&#x26;modificationDate=1684984787000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

**Step 4:** Check the connection from Kubectl to GreenNode Container:

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802494/Screen%20Shot%202021-05-24%20at%2010.40.43.png?version=1&#x26;modificationDate=1684984788000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

Thus, you have completed the initialization of Containers and connected to that Container right at your PC or Laptop.
