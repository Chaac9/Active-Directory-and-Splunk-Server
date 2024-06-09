# Downloading Splunk Universal Forwarder and Sysmon onto Windows Virtual Machines 

One of the first steps to be conducted is to change the name of the computers for both the Windows Server and Windows 10 Pro device, so that it will be easier to distinguish between these computers when analyzing their logs and events within the Splunk Dashboard.
* Within the Windows virtual machine, select the *File Explorer* icon and then right-click on **This PC** and then select **Properties**
  * Then when the *About* page opens up, you can rename the PC to something identifiable that will distinguish between the Windows server and Win-10 pro device on the Splunk dashboard.
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/e45b69e3-e625-4501-b6dc-cac74346b67b)

***
# Downloading Splunk Universal Forwarder onto the Window Devices

## Description 

The Splunk Universal Forwarders send telemetry data to the Splunk Server that was downloaded onto the Ubuntu Server Virtual Machine. In addition to downloading the agents for Splunk, we will also configure an index file from which only certain logs and events that may correlate with anomalous or malicious activity will be collected by the Windows devices. 

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
    * The file name is called **inputs.conf** and type is configured to **All Files**
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/2b4bd061-f06d-4e37-b973-c6ba84ce9e22)
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/12938fb1-e0b0-4508-9f5c-6a1677f426d1)


 * Once the **inputs.conf** is updated, the Universal Forwarder service must be restarted anytime the configuration file is updated
  * To do this, type in *services* in the Windows search bar  and select the **Run as administrator** option 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/b0c727ef-21d7-4c22-820b-4e5eee18e813)


 * Once in the *services* window find the **SplunkForwarder* service and select the **Properties** option after right-clicking on the service.
  * In the **General** tab ensure that the *Startup type:* is configured to **Automatic**
  * Under the **Service status:**  you can *Stop* the service and then *Start* it again to ensure the SplunkForwarder updates successfully.
  * In the *Services* page you can also select to **Restart** option, but if given the option that it cannot be restarted, then you can *Stop* and *Start* the service as another option to restart the service.
    
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/fd9e58cb-204f-4496-9f21-91790967013c)

# Downloading Sysmon onto the Windows Virtual Machines 

System Monitor is a Windows system service that logs system activity to the Windows Event log. Splunk can collect telemetry data from System Monitor (Sysmon). 

The first thing I did was download the Sysmon configuration file to be used during the application download of Sysmon on the Windows device, afterwards, I downloaded Sysmon from Microsoft and then executed the application with the configuration file 

***
## Configuration file for Sysmon to ensure only specific events crucial to Security are collected

I downloaded a system monitor (Sysmon) configuration file by GitHub user olafhartong. The reason for using this configuration file is to assist in reducing noise by not logging all events for Splunk to use, as well as ensuring only critical events that may be indicative of anomalous or malicious behavior are collected. In addition, this configuration file will also ensure system performance does not overload system resources by having it log every event. 

https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml
* When on the GitHub page, select the *Raw* option to open up the raw data on a different browser page to be downloaded
 * Right-click the page and select *save as* to save the configuration file as an XML file to any directory, from which you can access it soon.

*** 
To download System Monitor, go to your web browser and search for **sysmon by Sysinternals** 
* The first web link should be from Microsoft Learn, where the service can be downloaded
* https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon#Introduction
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/10a4b163-4ced-41ba-a6bb-4fbf116a9d26)

* Once downloaded, locate the compressed folder right-click the folder, and then selecting **Extract All..** to extract all files within the compressed folder
  
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/ea00625f-f42f-49a5-946d-2a2aa248efe2)

* When you see the uncompressed Sysmon folder, enter it and then copy the file path to be used in its download through Powershell with administrator privileges. 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/e0772da7-dc1f-4a18-998e-eb0e95b0e0f1)

* Open up Powershell with administrator privileges, and then type in **cd <filepath>**
 * Replace <filepath> in the command with the file path to the Sysmon folder that was uncompressed during its initial download from Microsoft. 

* Once in the directory for the uncompressed Sysmon folder, we will execute the Sysmon application to download with our Sysmon configuration file with the command **.\Sysmon64.exe -i ..\sysmonconfig.xml**

Go through the download to ensure it is configured on the device 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/a990ac97-e1de-4150-b30a-29d28cd51614)

* Ensure you restart the **Splunk Universal Forwarder** afterwards in *Windows Services* to ensure data is collected correctly for Sysmon

## Creating an Index in Splunk and Checking Logs from Splunk 

During the setup of the Splunk Universal Forwarder, an inputs.config file was configured so only specific logs were collected to be sent to Splunk.

Within that inputs.config file, it showed that all logs collected would be sent to a Splunk index named *endpoint* 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/be10393f-d063-4055-b5e4-2f9ef94d67c0)


Since the Splunk Universal Forwarder and Sysmon have been configured for both Windows devices (Windows Server 2022 and Windows 10 Pro), the next step would be to create an index called *endpoint* within the Splunk online dashboard for log analysis 
* The first step is to turn on the *Ubuntu Server* if it is not online, and log in.
* Afterwards, log in onto the Splunk Dashboard from any of the Windows OS devices
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/eaa93a06-05d0-4731-b7aa-4d719b0021b7)

* To Create an Index named *endpoint* head to **Settings** > **Indexes** > **New Index**
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/5bc74f20-d01e-4357-8215-3fe7ef91303e)

 * For the Index Name input *endpoint** and leave all other configuration options as default before saving and creating the index
 ![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/0eede5b7-8540-4410-b8c2-a42e88a6ca35)

* Now the Splunk Server will be configured to collect data from the Windows OS devices which have the Splunk Universal Forwarder
  * Head into **Settings** > **Forwarding and receiving** > **Configure receiving** > **New Receiving Port** 
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/6f3cb9ac-9632-40ee-b085-611df5ef0665)

 *  For the port, add **9997**, as that is the port used during the initial download setup for the Universal Splunk Forwarder
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/a8a13bb3-27f4-4e9a-b2d1-ec03429db94b)

Once everything has been set, collected logs from the Windows OS devices can be located using the index *endpoint* within *Search and Reporting* 
* In the Splunk platform go to **Apps** > **Search and Reporting**
  * Within the Search Bar input **index = endpoint** and  change the time frame to **All Time**
    * The reason why I changed the time frame is because there may have been no events collected within smaller time frames, for reasons such as the Windows virtual machines not being online during those smaller time frames
    * In the *fields* area, you can confirm that events are being collected from both Windows machines in the **Host** field
    
![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/bbc6331c-cb09-4fd7-9454-d30e7b9bd67e)

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/2d724936-545b-4265-b380-77d2ec2ed0f1)

