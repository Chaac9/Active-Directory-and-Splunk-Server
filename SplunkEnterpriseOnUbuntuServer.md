# Downloading Splunk Enterprise Server onto Ubuntu Server 

## Introduction 

In this part of the lab, I have downloaded the Splunk Enterprise Server from my host and enabled guest additions for VirtualBox to proceed with downloading Splunk Enterprise onto my Ubuntu Server virtual machine. By downloading guest additions for VirtualBox you can optimize the integration between the host machine and Ubuntu server virtual machine by enabling the sharing of directories to make it possible to have the Ubuntu Server access the folder in which the Splunk Enterprise downloaded into. 


The first step in downloading Splunk Enterprise is to login or sign-up and register to proceed with the download. Splunk Enterprise is available for 60 days and no credit card is required before downloading. The download process begins After logging on or registering head onto **Products** > **Free Trials and Downloads**
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/fba03828-fec9-4d53-9c8f-fed264bfcaf1)

Once in the Downloads section, find Splunk Enterprise and select the option **Get My Free Trial**. Then an installation package can be installed for Windows, Linux, and Mac OS; I have chosen the Linux installation package that is formatted as a **.deb** file. 
* The .deb formatted package is chosen because the Ubuntu Server is a Debian-based operating system, so the **.deb** formatted package is compatible with the Ubuntu virtual machine.

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/89bcc8dc-124a-4ddf-b352-35adcbca4f38)

The next step is to have the Ubuntu Server download the *VirtualBox-guest-additions-iso* file to enable file sharing between the machines. 
* In the command line terminal for Ubuntu type in the command **sudo apt-get install virtualbox**, and then hit the **TAB** key on the keyboard to see the available packages with the name *virtualbox* to install.
* The package to install is the *virtualbox-guest-additions-iso* one. Complete the previous command with the guest-additions part, and hit the **ENTER** key after. The full typed-in command is **sudo apt-get install virtualbox-guest-additions-iso**
  * Then hit the **y** key to confirm you want to download the guest-additions package. After, you will be prompted to enter your password for the Ubuntu server.
 ![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/148738d8-ed85-4c5b-8e14-f8c4fbf37ae4)
  * A GUI screen should present itself after downloading, press the **ENTER** key to complete the virtualbox-guest-additions download. 


* The next step is to add the Splunk Enterprise *.deb* package into the shared folders for the VirtualBox virtual machine of Ubuntu server to access.
  *  In the *Oracle VM VirtualBox Manager* select the Ubuntu Server virtual machine, select the gear icon labeled *Settings*, and then select the **Shared Folder** option.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/c63a7cc5-279d-4092-98f9-b9fe915e6fe3)
  * In the *Shared Folders* window select the folder icon that has a green plus sign
    * For the *Folder Path:* option select the drop-down icon and then select the Splunk Enterprise folder from your File management application.
    * The Folder Name will autocomplete  once you select the Splunk Enterprise package
    * Leave the *Mount point:* area blank
    * Select the *Read-only*, *Auto-mount*, and *Make Permanent* options to enable them
    * Then press *OK* to finalize your configurations for the shared folder 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/ff89ba16-dc6d-4f89-a9cc-aa8be341f030)


* Once the folder path for Splunk Enterprise has been added in the VirtualBox Manager, reboot the Ubuntu Server using the command **sudo reboot**. Once this is done, proceed with the download of VirtualBox guest additions to Ubuntu.
  * Once Ubuntu server has restarted type in the command **sudo apt-get install virtualbox-guest-utils**
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/b4efac41-7824-465c-8581-5ac8526594be)
  * Once you've entered the command, reboot the Ubuntu server again with **sudo reboot**
  * Once back in the command line terminal, Enter the command **sudo adduser <username> vboxsf**; replace the <username> part with the username of your Ubuntu server
    * This command allows your Ubuntu server to be added to the vboxsf group, and grant the user permission to access the shared folder
    * The *vboxsf* group is used by VirtualBox to grant access to shared folders
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/30865308-afcc-4986-9396-424b61f7d1db)


* The next step is creating a directory in Ubuntu to mount the shared folder containing the Splunk Enterprise server.
  *  Enter the command **mkdir share** to create a directory named *share*
  *  You can confirm the directory was created with the **ls -la** command 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/7080669c-8336-43f8-ae2e-083b72720dd9)

* Next, to mount our shared folder containing Splunk onto the *share* directory, use the command **sudo mount -t vboxsf -o uid=1000,gid=1000 <file> share/**; replace the <file> part of the command with the name of the shared folder from the VirtualBox manager.
  * To find the name of the shared folder, you can complete the same steps to add the shared folder in the *Shared Folder* section of VirtualBox Manager
    * In VirtualBox Manager select the Ubuntu Server virtual machine > Settings (gear icon) > Shared Folders > and select the Shared Folder under *Machine Folders*
  * Execute the command, then execute the command **ls -la** to ensure the shared folder was mounted, if done correctly then the *share* directory should be highlighted.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/ece1207d-1dbf-43c3-9260-196d5067a5c8)
 
* The following step is to head into the *share* directory to install the Splunk Enterprise server package
  * Execute the command **cd share**, and then enter **ls -la** to see what is within the *share* directory. You can find the Splunk Enterprise Debian package within this directory.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/cfb847ae-1b35-47d8-97bc-722662283673)


  * To download the Splunk Enterprise Debian package we will input the command **sudo dpkg -i splunk-9.2.1-78803f08aabb-linux-2.6-amd64.deb**
    * The Splunk name you download may be different due to it being a different version since when I downloaded the Splunk package
    * Instead of typing out the name of the whole Splunk Debian package, you can first just type **sudo dpkg -i splunk** and execute **TAB** so that the command autocompletes the part that contains Splunk.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/c24b0cd7-aef8-4642-a3e6-7ec3a4e8202c)

* Once Splunk Enterprise has been downloaded, locate splunk under the */opt/splunk* directory.
  * Execute the command **cd /opt/splunk** , and then execute **ls -la**
  * This will showcase the owner, user permissions, and details of the files and directories within the */opt/splunk* directory 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/fd3fee48-0582-4c48-87b0-370ab81c5f34)


* Continuing in the */opt/splunk* directory, we will act as the user *splunk*, as this is the user who is the owner with full permissions for the *bin* directory that will be used in the next step.
  * Execute the command **sudo -u splunk bash**, and then execute the command **cd bin** to enter the *bin* directory
    * The *bin* directory contains executables to start, stop, and manage Splunk services
  * While in the *bin* directory, execute the command **./splunk start**
    * This command starts up Splunk Enterprise
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/c85e816d-b2ef-4940-a4f6-4c916b195184)
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/da519949-53a5-4939-ba14-4e5796ae5e6a)
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/7f691b9f-4abd-4db9-a239-ad4b2b112619)

  * Once the installer for Splunk starts, you will be met with a license and agreement page, from which you can enter the **q** key to automatically scroll to the end of the agreement, and then enter **y** to accept the license and agreement.

* The final step is to ensure that every time the Ubuntu server virtual machine turns on it automatically starts Splunk Enterprise with the *splunk* user.
  * Execute this command while still in the /opt/splunk/bin directory: **sudo ./splunk enable boot-start -user splunk**
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/42dd8a15-34bf-414a-bf63-5874994cad42)
