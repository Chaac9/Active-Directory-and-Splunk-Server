# Virtual Machine Network Addressing and Configuration

## Introduction
In this file, I will show my actions to configure static IPs to the Windows Server 2022, Windows 10 Pro, and Ubuntu Server virtual machines. Having set the static IPs, the virtual machines then can communicate with each other within the **ADHomeLAB** NAT network and are given the ability to communicate with the internet. 


## Windows Server 2022 and Windows 10 Pro Static IP configuration
To ensure computer resources can communicate within a domain and the internet is to set the the static IPv4 configuration. 

The first step in a Windows operating system is to select the **globe with a cancel sign** icon on the bottom right of the window (as when first creating the virtual machine, there is no connectivity) and then selecting the *Network & Internet settings* option.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/7b1d5371-d36d-45f7-b1a2-1e0a3ce08065)

* Then I clicked the *Change adapter options* selection that is located under **Advanced network settings**
* Once the **Network Connections** window opens, select your virtual adapter by right-clicking it and then selecting *properties*
  ![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/62b065bd-ba6c-4ee5-b477-c57efb8bf359)
* In the adapter properties select *Internet Protocol Version 4 (TCP/IPv4)* and then select properties
* I finally configured my IPv4 settings by choosing the *Use the following IP address:* option, and set my IP address, subnet mask, default gateway, and preferred DNS server to match what I had put in the VirtualBox NAT Network and the network diagram I created showcasing the devices, connections, and data flow for this Active Directory Home Lab.
* Since the IPv4 prefix and subnet mask during the VirtualBox NAT network setup was 192.168.10.0/24, I had input **255.255.255.0** for the *Subnet mask* and **192.168.10.1** in the *Default Gateway* and *Preferred DNS Server* area. 
  * In my network diagram, I had selected **192.168.10.5** for the Windows Server virtual machine that acts as the domain controller, and **192.168.10.249** for the Windows 10 Pro virtual machine that had joined the domain; so these are the IP addresses I had input into the IPv4 properties for each respective virtual machine.

   
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/5e368961-64f0-47a0-8aa6-43042fc0ef4f)

* Once done setting the IPv4 configurations, I selected the highlighted *OK* window within the **IPv4 Properties** window and **exited** all other windows that were open to reach **IPv4 Properties**. 
 * The Network connection should then reset and you should be able to have internet connectivity
   
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/529c773f-4f17-49d4-adec-b0b453cec3ad)

## Ubuntu Server Static IP configuration

In my network diagram, I chose the IP address of **192.168.10.10** for my Ubuntu Server virtual machine and will showcase my actions to configure connectivity. 

When first logging into Ubuntu Server you will be met with a command-line terminal instead of a graphical user interface that can be seen on most Windows operating systems.
***
The first command I entered was to update and upgrade all repositories in the Ubuntu server to ensure all system package information and installed packages are up to date and upgraded to their latest versions.
* The command inputted was: **sudo apt get update && sudo apt get upgrade**
  * This command ensures system and installed packages are maintained for the security, stability, and functionality of the system 
***
Now to set the static IP on the Ubuntu Server, the steps are: 
* Type **sudo nano /etc/netplan/00-installer-config.yaml**
  * This command allows users to configure network interfaces within the /etc/netplan directory using the *00-installer-config.yaml* YAML file. 
  * It is within this directory where the Netplan utility is found to configure networking for cases such as configuring static IPs, DHCP, or defining DNS servers. 

* When the YAML file is opened, update the *dhcp4:* section to **no**
  * Then press *ENTER* on the keyboard to create a new line and press *TAB* **3** times before typing in an *addresses:* section underneath the *dhcp4:* section with the static IPv4 chosen for the Ubuntu Server
    * Ensure you add the subnet mask in the *addresses:* section in Classless Inter-Domain Routing (CIDR) notation; For example, my configuration was **[192.168.10.10/24]**.
  * Enter a new line for another section underneath *addresses:* and then press *TAB* **3** times before typing in a new section called *nameservers:*.
    * Press the space button on the keyboard, and then press *ENTER* and then press *TAB* **5** times to add another section underneath *nameservers:* that will also be called *addresses:* and input the DNS server of your choice; I input Google's DNS server **[8.8.8.8]**.
  * Press *Enter* on your keyboard to add another line and then press the *TAB* button on your keyboard  **3** times, from which you will then enter **routes:**.
    * Afterward, I pressed *Enter* and hit the *TAB* button **5** times before having typed in **-to: default**. 
  * Hit *Enter* another time and hit *TAB*  6 times, from which you will input your default gateway IP address with the section *via:*.
    *  I input **via: 192.168.10.1**, as this includes the default gateway I used.
 
 ![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/4644abe7-7b94-42cb-b3d5-d99d152ff934)

* After making all your configurations in the YAML file hold the *CTRL* and *X* buttons on your keyboard to exit the file, afterward press *Y* on the keyboard to save the changes made in the file.
  * Once you're back in the command-line terminal you can confirm changes were saved by typing in **sudo cat /etc/netplan/00-installer-config.yaml**  

 ![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/ea9795c4-0c6a-4eab-af5a-27e324952dd2)

* Input the command **sudo netplan apply** to ensure changes for networking configuration are effective in the Ubuntu Server system.
 * Then input the command *ip a* to display information regarding the network interfaces and confirm that the static IP is used

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/e48644e5-39f3-4333-b9d2-c2166e6145c1)


To confirm internet connectivity use the command *ping google.com*, and then press *CTRL* and *C* together to receive the statistics on whether the reachability of external networks is confirmed
* You can use any other website as well if you so choose. 

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/bcb6b960-fbde-4255-a3d5-4c16403a3433)
