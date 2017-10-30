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

Azure site to site VPN setup with BGP
------------------------------------

Mobile workstation setup
-------------------------
