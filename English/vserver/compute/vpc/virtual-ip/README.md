# Virtual IP

## Scenarios for Virtual IP <a href="#virtualip-scenariosforvirtualip" id="virtualip-scenariosforvirtualip"></a>

Add an Virtual IP to an instance is useful when you want to:

* Have a secondary or sub IP address in OS for some special use case (eg LVS, sub interface…)
* Create a low-budget, load-balance, high-availability solution.

## Virtual IP basics <a href="#virtualip-virtualipbasics" id="virtualip-virtualipbasics"></a>

A virtual IP address can be shared among multiple vServer Instance. An instance can have both private and virtual IP addresses, and you can access the instance through either IP address. A Virtual IP address has the same network access capabilities as a private IP address.

You can assign instances deployed in active/standby mode with the same Virtual IP address. Virtual IP addresses can work together with Keepalived to ensure high availability and disaster recovery. If the active instance is faulty, the standby instance automatically takes over services from the active one. It can be configured for HA or as load balancing clusters.

## Work with Virtual IP <a href="#virtualip-workwithvirtualip" id="virtualip-workwithvirtualip"></a>

#### Create Virtual IP <a href="#virtualip-createvirtualip" id="virtualip-createvirtualip"></a>

1. Go to GreenNode portal console, navigate to Virtual IP page
2. Select VPC and subnet for the Virtual IP address. Only instances in the same subnet with Virtual IP can be assigned to use the Virtual IP
3. After create you will get the IP information
4. Next step is assign Virtual IP to Instances, expand the detail of Virtual IP and go to tab **Address Pair Interface**, click **Add** **Address Pair Interface** and select Instances that you want to assign

#### Add/Remove Virtual IP to/from Instance <a href="#virtualip-add-removevirtualipto-frominstance" id="virtualip-add-removevirtualipto-frominstance"></a>

After create Virtual IP, you need to assign it to Instances:

1. Go to GreenNode portal console, navigate to Virtual IP page
2. Expand the detail of Virtual IP and go to tab **Address Pair Interface,** click **Add Address Pair Interface/Remove Address Pair Interface** and select Instances that you want to assign or remove
3. You will need to configure network from within instance to make Virtual IP works

#### Delete Virtual IP <a href="#virtualip-deletevirtualip" id="virtualip-deletevirtualip"></a>

1. Go to GreenNode portal console, navigate to Virtual IP page
2. Select Virtual IP and click **Delete** on the right side

<br>
