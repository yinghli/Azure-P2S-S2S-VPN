Azure-P2S-S2S-VPN
==========================================
This page will introduce how to transit point to site VPN to other regions using site to site VPN. <br>
Customer have multiple Azure region deployment. They have mobile worker connect to Azure by point to site VPN. <br>
Customer wants to single point of P2S VPN and extend the connectivity to all related Azure region. <br>

Toplogy
----------------
![](https://github.com/yinghli/Azure-P2S-S2S-VPN/blob/master/topology.PNG)

Customer have two region on Azure. <br>
One region is located at West Euro, VNET called P2S. The other is located at US East, VNET called S2S.<br>
VPN gateway in VNET P2S will terminate all point to site VPN from Internet mobile user. At the same time, this gateway will connect to other region by IPSec VPN. BGP will enable on this link to transit route from each gateway. <br>



Azure point to site VPN setup
------------------------------
In West Europe Region, we will use below parameter to setup VPN gateway. 
The detail setup can be found ![here](https://github.com/yinghli/Azure-P2S-VPN/blob/master/README.md)

Parameters            | Values
----------------------| -------------
VNET Name             | P2S
Address Space         | 10.5.0.0/16
Location              | West Europe
Subnet Address        | 10.5.1.0/24
GatewaySubnet         | 10.5.0.0/24
VPN Gateway Name      | P2S
VPN Type              | Route-based
VPN SKU               | VpnGw1
Azure BGP ASN         | 65501
Azure BGP Public IP   | 40.114.219.202
Azure BGP peer IP     | 10.5.0.254
P2S Client            | 10.6.0.0/24
P2S Authentication    | Radius
P2S Protocol          | IKEv2 / SSTP

Azure site to site VPN setup with BGP
------------------------------------
In US East Region, we will use below parameter to setup VPN gateway. 
We use BGP over IPSec to setup connectivity between VNET P2S and VNET S2S. 

Parameters            | Values
----------------------| -------------
VNET Name             | S2S
Address Space         | 10.0.0.0/16
Location              | US East
Subnet Address        | 10.0.0.0/24
GatewaySubnet         | 10.0.1.0/24
VPN Gateway Name      | S2S-US-East
VPN Type              | Route-based
VPN SKU               | VpnGw1
Azure BGP ASN         | 65502
Azure BGP Public IP   | 13.90.85.209
Azure BGP peer IP     | 10.0.1.254

Mobile workstation setup
-------------------------
