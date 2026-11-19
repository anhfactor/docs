# Connect to virtual server

Users have many ways to connect to the virtual server such as the Console function on GreenNode Portal or other client tools. Depending on the operating system of the virtual server, the operating system of the personal machine or the desired connection type, you can select the appropriate connection method.

### **Connect using GreenNode Portal console** <a href="#connecttovirtualserver-connectusingvngcloudportalconsole" id="connecttovirtualserver-connectusingvngcloudportalconsole"></a>

This method requires you to have the server's password. By default, the GreenNode system automatically generates a password for the virtual server when you create a new one. This information will be emailed when the virtual server is created and is in Active state. You can also use the username and password you entered earlier in the server creation process.

Some cases need to use this connection method to solve, such as:

* The server has a network connection problem
* When it is necessary to find out the problem and handle it, the abnormal programs running on the server cause network congestion or CPU processing is too high.
* The server has an incorrect firewall configuration

#### How to do it <a href="#connecttovirtualserver-howtodoit" id="connecttovirtualserver-howtodoit"></a>

1. Log in to GreenNode portal and go to vServer service page
2. On the Instances page, specify the server you want to connect to, at the Selection Menu on the right, select Console to open the server management window via the console
3. You will need the server's operating system password to log in.\\
4. You can also call the keyboard shortcut CTRL+ALT+DEL to restart the server by clicking the Send CtrlAltDel button in the upper right corner

***

### **Connect to a Windows server using the Remote Desktop tool** <a href="#connecttovirtualserver-connecttoawindowsserverusingtheremotedesktoptool" id="connecttovirtualserver-connecttoawindowsserverusingtheremotedesktoptool"></a>

Remote Desktop Protocol (RDP) requires user and password information for simple authentication when accessing the server

#### Request <a href="#connecttovirtualserver-request.1" id="connecttovirtualserver-request.1"></a>

Before connecting to a Windows server, you need to ensure the following requirements:

* Windows server is in Running state, otherwise, you need to restart the server
* You need the password to connect to the Instance, if you did not provide the password information when creating the server, you can use the account information and the automatically generated password sent in the email
* The virtual server must have a working network connection
* The Security Group setting needs to be defined as allowing traffic on port tcp/3490 for the RDP protocol

#### How to do it <a href="#connecttovirtualserver-howtodoit.2" id="connecttovirtualserver-howtodoit.2"></a>

[Remote Desktop vào Server Windows HCM 03](2.-remote-desktop-to-windows-server-hcm-03.md)

***

### **Connect to a Linux server using the SSH Client tool** <a href="#connecttovirtualserver-connecttoalinuxserverusingthesshclienttool" id="connecttovirtualserver-connecttoalinuxserverusingthesshclienttool"></a>

Users can use the operating system password or SSH key pair to connect to the server via the SSH protocol.

When making connections to a Linux server, you should prefer the method of using SSH key pairs and tools that support the SSH protocol such as Linux terminal or PuTTY on Windows. This is the most secure and convenient method to connect to the server.

#### Request <a href="#connecttovirtualserver-request" id="connecttovirtualserver-request"></a>

* The SSH key pair must be pre-generated into the declaration in the VM new creation procedure
* The Linux server that needs to connect to must be
* Active Virtual servers need to have a proper network connection, for example using Floating IP to connect to the internet directly
* A Security Group setting is declared and this security group is attached to the server to be connected to allow smooth traffic. Specific settings such as allow traffic port tcp/234 for SSH protocol

#### How to do it <a href="#connecttovirtualserver-howtodoit.2" id="connecttovirtualserver-howtodoit.2"></a>

[SSH login to Server Linux HCM03](1.-ssh-login-to-server-linux-hcm-03.md)

