# Active Directory and Splunk Server

## Introduction

    This project involves configuring Active Directory within Windows Server 2022, adding Active Directory Domain Services, connecting an endpoint to a newly created domain, and then having telemetry and logs from these endpoints be sent to a Splunk Server configured on an Ubuntu Server. After the Windows Server 2022 virtual machine had Active Directory Domain Services set up, users and groups were created. I then connected a Windows 10 pro endpoint to the domain and logged in as a domain user. Once the Splunk Server was configured on the Ubuntu Server, Splunk Universal Forwarders agents were downloaded onto the Window OS endpoints to send telemetry to the Splunk Server. I then logged into the Splunk Server platform on a web browser to perform log analysis of events and attacks performed on the Windows endpoints.

Architecture of the Active Directory and Splunk Server connection Home Lab:
- Active Directory
- Active Directory Domain Services
- Splunk Server
-   Splunk Universal Forwarder Agents
    - A lightweight component of Splunk Enterprise used to collect and forward data to a centralized Splunk instance indexer, from which log analysis can be performed from the endpoints that have the Universal Forwarder downloaded.
        - https://www.splunk.com/en_us/blog/learn/splunk-universal-forwarder.html
