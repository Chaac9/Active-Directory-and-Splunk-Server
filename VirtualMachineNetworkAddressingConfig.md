# Virtual Machine Network Addressing and Configuration

## Introduction
In this file, I will show my actions to configure static IPs to the Windows Server 2022, Windows 10 Pro, and Ubuntu Server virtual machines. Having set the static IPs, the virtual machines then can communicate with each other within the **ADHomeLAB** NAT network and are given the ability to communicate with the internet. 


## Windows Server 2022 Static IP configuration
To ensure computer resources can communicate within a domain and the internet is to set the the static IPv4 configuration. 

The first step in a Windows operating system is to select the **globe with a cancel sign** icon on the bottom right of the window (as when first creating the virtual machine, there is no connectivity) and then selecting the *Network & Internet settings* option.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/7b1d5371-d36d-45f7-b1a2-1e0a3ce08065)

* Then I clicked the *Change adapter options* selection that is located under **Advanced network settings**
* Once the **Network Connections** window opens, select your virtual adapter by right-clicking it and then selecting *properties*
  * ![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/62b065bd-ba6c-4ee5-b477-c57efb8bf359)
* In the adapter properties select *Internet Protocol Version 4 (TCP/IPv4)* and then select properties
* I finally configured my IPv4 settings by choosing the *Use the following IP address:* option, and set my IP address, subnet mask, default gateway, and preferred DNS server to match what I had put in the VirtualBox NAT
