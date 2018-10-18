---
title: SAP NetWeaver on SQLServer 
description: The NetWeaver on SQL Server application solution illustrates how a user request flows through an SAP landscape built on NetWeaver by utilizing Azure Virtual Machines to host SAP applications and a SQL Server database.
author: adamboeglin
ms.date: 10/18/2018
---
# SAP NetWeaver on SQLServer 
This NetWeaver on SQL Server application solution illustrates how a user request flows through an SAP landscape built on NetWeaver using Azure Virtual Machines to host SAP applications and a SQL Server database. This system takes advantage of OS clustering for high availability, premium storage for faster storage performance and scalability, SQL Server AlwaysOn capability for replication, and a full disaster recovery (DR) configuration for 99.95 percent system availability.

## Architecture
<img src="media/sap-netweaver-on-sql-server.svg" alt='architecture diagram' />

## Data Flow
1. Using Azure Active Directory synchronized with on-premises Active Directory, SAP application user authenticates from on-premises to SAP landscape on Azure with single sign-on credentials.
1. Azure high speed Express Route Gateway connects on-premises network to Azure virtual machines and other resources securely.
1. Sales order request flows into highly available SAP ABAP SAP Central Services (ASCS), and then through SAP application servers running on Azure Virtual Machines scale out file server in an Azure VM
1. The request moves from the SAP app server to SQL Server running on a primary high-performance Azure VM.
1. Primary (active) and secondary (standby) servers running on SAP certified virtual machines are clustered at OS level for 99.95 percent availability.  Data replication is handled through SQL Server AlwaysOn in synchronous mode from primary to secondary, enabling zero Recovery Point Objective (RPO).
1. SQL Server data is persisted to high-performance Azure Premium Storage.
1. SQL Server data is replicated Disaster recovery virtual machine in another Azure region through Azures high speed backbone network and using SQL Servers AlwaysOn replication in asynchronous mode. The disaster recovery VM can be smaller than the production VM to save costs.
1. VMs on the disaster recovery region can be used for nonproduction work to save costs.
1. SAP app server with ASCS on disaster recovery side can be in standby shutdown mode, and can be started when needed to save costs.

## Components
* Information on [Virtual Machines](http://azure.microsoft.com/services/virtual-machines/) for SAP application servers.
* Microsoft Azure [Premium Storage](http://azure.microsoft.com/services/storage/disks/) provides improved throughput and less variability in I/O latencies. For improved performance, [Premium Storage](http://azure.microsoft.com/services/storage/disks/) uses solid state disk (SSD) in Azure Storage nodes, and read cache that's backed by the local SSD of an Azure compute node.

## Next Steps
* [SAP Certifications for Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-certifications)
* [Premium Storage: high-performance storage for Azure Virtual Machine workloads](https://docs.microsoft.com/azure/storage/storage-premium-storage)