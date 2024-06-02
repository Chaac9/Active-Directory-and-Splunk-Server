# Network Configuration of VirtualBox Virtual Machines

 ## Introduction
In this file, I will provide steps on how I configured my virtual machines containing Windows Server 2022, Windows 10 Pro, and Ubuntu Server, as well as static IPs within these VMs to communicate with one another within an internal Network and the internet. 

## VirtualBox Network Setup
Within VirtualBox, a NAT Network is created to ensure all endpoints can communicate effectively within the internal and external networks (Internet access) by enabling their network adapter and attaching their adapter to this NAT network.

The steps to creating the NAT Network used by the endpoints in this Active Directory home lab are as follows: Select the 'Network' Manager Tool after selecting the drop-down list from the Global **Tools** banner above your virtual machine list.

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/5fb22242-a5e4-4d04-b7f9-29e3b262d0e0)





Within the **Networks** tab select the *Create* option to add a new host-only network to the list. You should then see a new NAT network named *NatNetwork* populate the area under the **NAT Networks** tab and see its properties under the **General options** tab. Then, in the **General Options** tab, you can configure the network address and subnet mask within the *IPv4 Prefix:* area for the NAT service interface, and enable DHCP. You can also rename your NAT network, and enable IPv6 if you choose.

For the NAT Network properties I chose for this Active Directory lab, I changed my IPv4 prefix to contain the network address of **192.168.10.0** with the subnet mask **/24**, renamed the network to *ADHomeLab*, and enabled DHCP.

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/88e765d8-46ef-4fc3-a28b-803ad2803dd1)

## Connecting Virtual Machines to the NAT Network on VirtualBox

After configuring my NAT network **(192.168.10.0/24)** I enabled the virtual network adapters of my virtual machines to attach to my **ADHomeLab** NAT Network.
The steps for this include: select  the virtual machine > selecting the *Settings* option > heading to the *Network* tab > enabling the *Enable Network Adapter* option, attaching to the **NAT Network** option, and selecting the NAT Network name, mine being **ADHomeLAB**

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/b4ed1985-a640-4e72-9ea6-9c8bbdff9a9f)

## References 
* https://www.virtualbox.org/manual/ch01.html#gui-tools
* https://www.virtualbox.org/manual/ch06.html#network_nat_service
* https://www.virtualbox.org/manual/ch06.html#network-manager
* https://www.virtualbox.org/manual/ch06.html#network-manager-nat-network-tab
