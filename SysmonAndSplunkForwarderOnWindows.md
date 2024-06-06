# Downloading Splunk Universal Forwarder and Sysmon onto Windows Virtual Machines 

One of the first steps to be conducted is to change the name of the computers for both the Windows Server and Windows 10 Pro device, so that it will be easier to distinguish between these computers when analyzing their logs and events within the Splunk Dashboard.
* Within the Windows virtual machine, select the *File Explorer* icon and then right-click on **This PC** and then select **Properties**
  * Then when the *About* page opens up, you can rename the PC to something identifiable that will distinguish between the Windows server and Win-10 pro device on the Splunk dashboard.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/e45b69e3-e625-4501-b6dc-cac74346b67b)

***
# Downloading Splunk Universal Forwarder onto the Window Devices

## Description 

The Splunk Universal Forwarders are used to send telemetry data to the Splunk Server that was downloaded onto the Ubuntu Server Virtual Machine. In addition to downloading the agents for Splunk, we will also configure an index file from which only certain logs and events that may correlate with anomalous or malicious activity will be collected by the Windows devices. 

* While in either of your Windows virtual machines, the first step to download the Universal Forwarder is to go back to the Splunk website, log in, and then head into *Products* > *Free Trials and Downloads*
  * Afterwards head to the *Universal Forwarder* section and select the *Get My Free Download* option.
  * You can then select the Windows Installation package; The Windows Server will be a *x64-bit* package that will be downloaded while the Windows 10 Pro device will depend on whether you configured the virtual machine to be a x32-bit system or a x64-bit system
    * To determine if the Windows 10 machine is a x32-bit or x64 bit system, head into the *About* page of your device, from where you changed the *device name*; you will see it in the *System type* section, like in the the first image above

* Once the Splunk Universal Forwarder is downloaded and the installation window opens, accept the license and agreement and select the *An on-premises Splunk Enterprise instance*
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/194f1d25-96b3-498a-91d8-7e1068637045)

  * The next page asks for you to input a user name, I input **admin** for mine
    * This username will be used when accessing the Splunk dashboard from which we can generate reports and analyze telemetry data sent from the Windows devices.
    * The next page involving the *Deployment Server* can be skipped, just select **Next**
    * On the *Receiving Indexer* page, input the IP of the Ubuntu Server that contains Splunk Enterprise, and for the port of the receiving indexer input **9997** instead of the default provided in the description
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/d15b5124-a14d-4c4c-95ab-822535859050)
***

Once the Universal Forwarder has successfully downloaded, an input configuration (inputs.conf) file will be created to ensure that only certain events are sent over to Splunk.

* To create and configure this inputs file, head into *File Explorer* and then select the drop-down menu for *This PC* 
  * Then select the **Local Disk (C:)** option > select **Program Files** > **SplunkUniversalForwarder** > **etc** > **system** > **local**
    * The *inputs.conf* file will be created within the *local* directory  
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/2b4bd061-f06d-4e37-b973-c6ba84ce9e22)


