# SSH Key (Key pairs)

A key pair, consisting of a public key and a private key, is a set of security credentials that you use to prove your identity when connecting to an vServer instance. For Linux instances, the private key allows you to securely SSH into your instance.

Anyone who possesses your private key can connect to your instances, so it's important that you store your private key in a secure place.

When you launch an Linux instance, you are prompted for a key pair. When your instance boots for the first time, the public key that you specified at launch is placed on your Linux instance in an entry within \~/.ssh/authorized\_keys. When you connect to your Linux instance using SSH, to log in you must specify the private key that corresponds to the public key. For more information about connecting to your instance, see {Connect to instance page}.

There is no way to recover a private key if you lose it. You can use GreenNode Portal to create your key pairs. You can also use a third-party tool to create your key pairs, and then import the public keys to GreenNode. GreenNode supports ED25519 and 2048-bit SSH-2 RSA keys for Linux instances.

This topic describes how to create, delete and import a key pair.

### **Create a SSH Key** <a href="#sshkey-keypairs-createasshkey" id="sshkey-keypairs-createasshkey"></a>

The first thing you can do with your SSH Key is create a new one. Click the "Create SSH Key" button in the upper left corner. You will be redirected back to the creation page to enter the necessary information to create. Here you can create SSH Key using our intuitive editor with user-friendly interface.

### **Import a SSH Key** <a href="#sshkey-keypairs-importasshkey" id="sshkey-keypairs-importasshkey"></a>

If you do not have an SSH Key on GreenNode Portal, you must create a new SSH Key to use for authentication. If you already have SSH Key on your own store, you can click the "Import SSH Key" button, the interface will appear a page that allows you to enter SSH Key information, enter the SSH Key name and paste the Public Key into the corresponding field to complete the SSH Key input.

### **Delete a SSH Key** <a href="#sshkey-keypairs-deleteasshkey" id="sshkey-keypairs-deleteasshkey"></a>

If there is an SSH Key you want to delete, select an SSH Key and click the "Delete" button in the upper right corner. A confirmation method will appear to make sure you don't delete it by mistake because once deleted, the SSH Key cannot be recovered.
