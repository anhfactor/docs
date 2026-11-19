# External Interfacêm

### **Scenarios for External Interface** <a href="#externalinterface-scenariosforexternalinterface" id="externalinterface-scenariosforexternalinterface"></a>

Attaching an External Interface to an instance is useful when you want to:

* Have a direct IP address in OS for some special protocol (Eg SIP…)
* Build your own Firewall or VPN gateway with the instance that have internal and external interface
* Create a low-budget, high-availability solution.

### **External Interface basics** <a href="#externalinterface-externalinterfacebasics" id="externalinterface-externalinterfacebasics"></a>

You can create an external interface, attach it to an instance, detach it from an instance, and attach it to another instance. When you move a external interface from one instance to another, network traffic is redirected to the new instance.

You need to configure IP address for External Interface from within instance, static or DHCP configuration will work. You can only attach External Interface to Instance that is not associated with Floating IP.

{% hint style="warning" %}
If you set a custom MTU on the external NIC, keep MTU **< 4000 bytes**. Larger MTU can cause packet loss when traffic goes out via External Interface. For Internet-facing traffic, keep MTU at `1450` (or smaller if needed). See [MTU & “DF flag” best practice on GreenNode](../../../vmarketplace/network-software-installation/pfsense-on-hcm03/mtu-and-df-flag-best-practice-on-vng-cloud.md).
{% endhint %}

### **Work with External Interface** <a href="#externalinterface-workwithexternalinterface" id="externalinterface-workwithexternalinterface"></a>

#### Create External Interface <a href="#externalinterface-createexternalinterface" id="externalinterface-createexternalinterface"></a>

1. Go to GreenNode portal console, navigate to External Interface page
2. Create External Interface, you can check the price on right panel.
3. After create you will get the IP information including address, netmask and gateway, these informations need for operation later.

#### Attach/Detach to/from Instance <a href="#externalinterface-attach-detachto-frominstance" id="externalinterface-attach-detachto-frominstance"></a>

1. Go to GreenNode portal console, navigate to Instance page
2. Go to detail of the Instance that need to attach the External Interface, go to tab Network Interface
3. Click **Attach an Interface** and select your existing External Interface. In case of Detach, just confirm the action after click **Detach an Interface**.
4. After attach the External Interface, you must configure network from within instance with its information.

#### Delete External Interface <a href="#externalinterface-deleteexternalinterface" id="externalinterface-deleteexternalinterface"></a>

1. Go to GreenNode portal console, navigate to External Interface page
2. Select the External Interface to delete, click **Delete** on right side.

<br>
