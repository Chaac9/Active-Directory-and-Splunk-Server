# Active Directory and Splunk Server

## Introduction

This project involves configuring Active Directory within Windows Server 2022, adding Active Directory Domain Services, connecting an endpoint to a newly created domain, and then having telemetry and logs from these endpoints be sent to a Splunk Server configured on an Ubuntu Server. After the Windows Server 2022 virtual machine had Active Directory Domain Services set up, users and groups were created. I then connected a Windows 10 pro endpoint to the domain and logged in as a domain user. Once the Splunk Server was configured on the Ubuntu Server, Splunk Universal Forwarders agents were downloaded onto the Window OS endpoints to send telemetry to the Splunk Server. I then logged into the Splunk Enterprise platform on a web browser to perform log analysis of events and attacks performed on the Windows endpoints.

Architecture of the Active Directory and Splunk Server connection Home Lab:
- Active Directory
- Active Directory Domain Services (AD DS)
    - Active Directory Domain Services is a feature provided by Windows Server that is a distributed database for centralized management of organizational units (OUs) such as users, groups, or computers. Through logon authentication, domain users can access resources; and administrators can regulate access to resources using access controls features and perform policy-based adminisiration to efficiently manage complex networks.
        -  https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831484(v=ws.11)
- Splunk Enterprise Server
    - Splunk Enterprise is software that performs data ingestion from several sources such as endpoints, applications, or websites. Once data sources are defined, data is processed and stored to be indexed into events that can be searched for within a web dashboard. Within the Splunk web dashboard, alerts and reports can be generated as well to perform more detailed analysis on events and whether a true positive attack or breach has occured.
        - https://docs.splunk.com/Documentation/Splunk/9.2.1/Overview/AboutSplunkEnterprise
-   Splunk Universal Forwarder Agents
    - A lightweight component of Splunk Enterprise used to collect and forward data to a centralized Splunk instance indexer, from which log analysis can be performed from the endpoints that have the Universal Forwarder downloaded.
        - https://www.splunk.com/en_us/blog/learn/splunk-universal-forwarder.html
        - https://docs.splunk.com/Documentation/Forwarder/9.2.1/Forwarder/Abouttheuniversalforwarder

![image](https://github.com/Chaac9/Active-Directory-and-Splunk-Server/assets/98796264/b92ff215-4b56-4153-ae4e-899835bf5208)
