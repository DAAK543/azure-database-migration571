# Project:  AZURE DATABASE MIGRATION 



## Introduction 

The aim of this project is to architect and implement a cloud-based database system on Azure via hands-on expertise in cloud engineering. A production environment was set-up for the AdventureWorks database using the Microsoft SQL Server Management Studio (SSMS) and was subsequently migrated to Azure SQL database.




## Usage




## Documentation

## Milestone 1: Set up the Environment



### Task 1: Set up a github repo

A github repo was set up on github through VScode to update changes on the repo and track changes on github.

The name of the applicable github repo is https://github.com/DAAK543/azure-database-migration571




### Task 2 

Azure account credentials from AiCore support.

A free account subscription was created by clicking the appropriate link on the site.

The following Azure services were created as per image below


![Alt text](image-21.png)


![Alt text](image-22.png)

Some of the services created were virtual machine, server, resource group, sql database, and storage account.


- Virtual machine: adventure-vm
- Resource group: adventure-database-rg
- Resource group: adventure-storage-rg
- Sql server: adventure-skylight
- Storage account: adventure1storage
- SQL database: adventure-database




## Milestone 2: Set up the Production Environment



### Task 1 - Provision a Windows Virtual Machine

Windows virtual machine called adventure-vm was created on Azure

see details below:


![Alt text](image-23.png)




### Azure Storage and Container created

The storage account created on Azure is called adventure1storage and container called adventure1container.

Please see images of adventure1storage and adventure1container below respectively.


![Alt text](image-24.png)


![Alt text](image-25.png)




### Task 2 - Connection to Windows Virtual Machine

Appropriate firewall configuration done was done through VSCode to enable adventure-skylight server and adventure-database connection on VSCode, microsoft remote desktop installed and RDP protocol deployed to facilitate connection with the VM.




### Task 3 - Install SQL server and SSMS on the Virtual Environment

### Installation of SQL Server

An SQL database data called adventure-database and server called adventure-skylight were created on Azure with an SQL server log in authentication method.

The adventure-database was associated with adventure-skylight server and adventure-database-rg (resource group)

See image below:


![Alt text](image-26.png)


The adventure-database was connected via VSCode. To achieve this connection, an SQL server extension was installed on VSCode.The SQL server connection was added on VSCode and the server name link (adventure-skylight.database.windows.net) was pasted on the server name field on VSCode. Appropriate log in authentication credentials were also inputted (username and password). 

See image of adventure-skylight server connection on VSCode SQL server below:


![Alt text](image-27.png)


The SQL server installed via the VSCode extension is called Microsoft SQL Server (mssql)


A firewall rule was configured through VSCode to enable public access and access to public network was enabled on Azure for selected networks. 

Note: The start and end IP addresses for the firewall rule configuration must be the same to generate a firewall rule name.



### Installation of SQL Server Management Studio (SSMS)

SSMS is a graphical interface tool provided by Microsoft to manage SQL server instances and databases.

- Download the SQL server developer setup from this link https://go.microsoft.com/fwlink/p/?linkid=2215158&clcid=0x809&culture=en-gb&country=gb


- Select basic installation type as per image below:


![Alt text](image-5.png)


- Accept license terms


- Choose installation location and click install as per image below:


![Alt text](image-7.png)

- Download the free SSMS version 19.1 from link https://aka.ms/ssmsfullsetup

- Follow on-screen instructions and verify SQL server installation.


Installation was done on the virtual machine with server name corresponding to adventure-vm as per image below


![Alt text](image-28.png)


The SSMS was launched by clicking the connect button in the image above. With a successful connection to the server, an Object explorer window was opened revealing the highlighted SQL server instance name as per image below.


![Alt text](image-29.png)


### Task 4 - Creation of Production Database

The production database was created by restoring it from the backup file in the link below                                   

https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak

The backup file corresponds to the Microsoft Sql server database known as Adventureworks2022.

Restoring the AdventureWorks2022 database from the backup file replicates an authentic production database environment. 

## Process

- Launch Sql server management studio (SSMS)

- Connect to server

- Click on the backup file link provided to download it on the remote desk

- On the object explorer page, right-click on databases as per image below and click on Restore Database 

![Alt text](image-30.png)

- Select device option and follow instruction in the image below and click add to add file

![Alt text](image-16.png)

- Add adventurewWorks2022.bak and click ok 

- Tick restore and click ok - A message is generated that states "AdventureWorks2022 restored successfully"
See images of database and tables below

![Alt text](image-31.png)



## Mileston 3 - Migrate to Azure SQL Database




### Task 1 - Set Up Azure SQL Database 

Azure SQL database created earlier is called the adventure-database and serves as the target for migrating the on-premises database (AdventureWorks2022). All appropriate firewall rules, authentication and IP address were previously configured to facilitate ease of connection.




### Task 2 - Prepare for Migration

Azure Data Studio was installed on my local computer using the link below 

https://colab.research.google.com/corgiredirector?site=https%3A%2F%2Fgo.microsoft.com%2Ffwlink%2F%3Flinkid%3D2242848


Following the installation of Azure Data Studio, two server connections were made.

- Connection to the on premise server: adventure-vm 

- Connection to the cloud server: adventure-skylight 

See image below:

![Alt text](image-32.png)




### Task 3 - Connect to SQL Database

Connection to the Azure cloud server was achieved using the required login credentials for adventure-skylight and adventure-database selected as detabase. While connection to the on-premises server (adventure-vm) was achieved using windows authentication and AdventureWorks2022 as selected database.  




### Task 4 - Schema Migration

Following the connection of the on-premises database and Azure SQL database, to achieve schema migration, SQL Server Schema Compare was installed on Azure Data Studio via the extension option. After installation of the SQL Server Schema Compare, the local database (AdventureWorks2022) was right-clicked to select the schema compare option. 


As seen in the image below after selecting the schema compare option, the source and target databases were appropriately confirmed. in this case, the source database was AdventureWorks2022 and applicable applicable server while the target database was adventure-database and its applicable server. Click the ok button to continue.

![Alt text](image-33.png)



Also, at the top of the Schema compare page, the compare button was clicked to synchronize the schema between Azure database and the local database. 

![Alt text](image-34.png)



Below is the outcome of the schema compare - adventure-database definitely had no data.


![Alt text](image-35.png)


Selected schema on the AdventureWorks database above was applied to the target database (adventure-database) to synchronize schema between the on-premises database and the Azure SQL database by clicking the Apply button

![Alt text](image-36.png)




### Task 5 - Data Migration

Azure SQL Migration tool was installed via Extension option by searching for Azure SQL Migration through Extension view on Azure Data Studio.

On the Azure Data Studio, the on-premises server (adventure-vm) right-clicked and manage option selected to access the Azure SQL Migration. See image below.

![Alt text](image-37.png)


Azure SQL was accessed by clicking on Azure SQL Migration under General and AdventureWorks2022 was selected as per image below follwed by clicking next.

![Alt text](image-38.png)


Follow subsequent instructions, select target platform (Azure SQL Database) and tick AdventureWorks database as per image below.


![Alt text](image-39.png)


Details of Azure SQL target were filled before connection was done. 

Source database - AdventureWorks
Target database - adventure-database

Also, an Azure Database Migration Service was created on Azure account and was configured for migration on Azure Data Studio  - see images below.


![Alt text](image-40.png)


![Alt text](image-44.png)


![Alt text](image-42.png)


![Alt text](image-43.png)


An integration runtime was setup as per instructions and one of the authentication keys provided was used to register the self-hosted integrated runtime created to facilitate connectivity between source and target databases. Link downloaded https://aka.ms/sql-migration-shir-download


![Alt text](image-45.png)


![Alt text](image-46.png)


 The next instructions was to input the on-premises server password, select edit tables and tick Table name. Schema was found on target and validation was done.


 ![Alt text](image-47.png)


 ![Alt text](image-48.png)


 ![Alt text](image-49.png)


Migration was done by clicking next after validation had been done. See below.


![Alt text](image-50.png)


![Alt text](image-51.png)


![Alt text](image-52.png)


Migration was successful! As per image above.



## Milstone 4 - Backup and Restore

Regular and consistence backup of the Azure SQL Database is critical for data protection. Whereas, irregular backups could result in reputational damage, incresed downtime, inadequate disaster recovery, and the risk of high data loss.

### Task 1  - Backup of the On-Premise Database (AdventureWorks2022)

The aim of this backup process is to restore the database later to a development environment where developers can work on testing and developing new features.

Process

- Open SQL Server Management Studio (SSMS) and connect to the SQL server instance hosting the AdventureWorks2022 database


![Alt text](image-53.png)


- Right-click on the AdventureWorks2022 database, select Tasks and Backup option. 


![Alt text](image-54.png)


- A full Backup option was selected as per the image above. Backup Destination selected was Disc and the default Backup Path as per the backup folder.

Backup was done by clicking OK - See image below.


![Alt text](image-55.png)


The Backup of AdventureWorks2022 was successful as per image above.


Backup file storage location - see image below

![Alt text](image-56.png)


## Task 2  - Upload Backup to Blob Storage

Storage account and container initially created on Azure were adventure1storage and adventure1container - see image below.

![Alt text](image-57.png)


To move the recent backup of AdventureWorks2022 database to adventure1container for Blob storage, the upload button of adventure1container was clicked to reveal the upload blob area and the recent AdventureWorks2022 database backup file was dragged from the relevant file location and dropped in the upload blob area. 

![Alt text](image-58.png)


![Alt text](image-59.png)


![Alt text](image-60.png)


Blob size, type, access tier and file were left as default setting. Upload was done.

Upload of the AdventureWorks2022 backup file to the storage blob was successful - see image below


![Alt text](image-61.png)


See properties of the blob in the image below.


![Alt text](image-62.png)


The blob can be accessed by copying the URL  - see below

https://adventure1storage.blob.core.windows.net/adventure1container/AdventureWorks2022.bak



## Task 3 - Restore Database on Development Environment

The development environment is believed to be a controlled and isolated environment in software development much like a sandbox for testing, developing and experimenting applications with no impact on the production environment.


The development environment was provisioned by creating a new Windows virtual Machine and SQL Server was installed to replicate the necessary database infrastructure.

New VM created is called Dragon-vm. See image below

![Alt text](image-63.png)

SQL Server setup downloaded from link  https://go.microsoft.com/fwlink/p/?linkid=2215158&clcid=0x809&culture=en-gb&country=gb 

Download the free SSMS version 19.1 from link https://aka.ms/ssmsfullsetup

Follow on-screen instructions and verify SQL server installation.

Launch Dragon-vm server - see image below


![Alt text](image-64.png)


![Alt text](image-65.png)


Right-click on Databases in the object explorer to restore the recent AdventureWorks database backup file. 

Select Device and URL option. To access the URL in the storage blob, browse Azure storage container with relevant authentication credentials for access. 

![Alt text](image-66.png)


adventure1storage was selected as Storage account and adventure1container selected as Blob container.

Shared access signature was generated by clicking the Creat credential button. See image below


![Alt text](image-67.png)


Click Ok button and follow instruction. AdventureWorks database backup file in the Storage blob on Azure is being replicated added in the Dragon-vm backup folder. See images below.


![Alt text](image-68.png)


![Alt text](image-69.png)


![Alt text](image-70.png)


![Alt text](image-71.png)


Backup was successful. AdventureWorks database was replicated on the Dragon-vm server. See image below.


![Alt text](image-72.png)


![Alt text](image-73.png)



### Task 4 - Automate Backups for Development Database


Creating a weekly backup schedule for the AdventureWorks2022 database in the development environment

- In the object explorer, click on Management tab and right-click on MaintenancePlans


![Alt text](image-74.png)


- Enable the SQL Server Agent through the SQL sever Configuration Manager from the Start Menu search option, click on SQL services and right-click on SQL Server Agent to click start. See image of SQL Server Agent below after enablement.


![Alt text](image-76.png)


- Right-click on MaintenancePlans and select Maintenance Plan Wizard and click next as per image below.


![Alt text](image-77.png)


- Give the Plan a name. I gave the Plan the name MaintenancePlanFullBackup. Proceed to schedule backup by clicking change option. See images below.


![Alt text](image-78.png)


![Alt text](image-79.png)


As per the above image, the maintenance plan was scheduled weekly on Sundays at 12:00:00 AM commencing from 7th January 2024. No end-date was selected unless configured otherwise. Selected Start-time 12:00:00 AM and End-time 11:59:59 PM assuming no business operations on Sundays.

Follow the next instruction and tick Back Up Full Database (Full) under Select Maintenance Tasks and click Next. See image below.


![Alt text](image-80.png)


On the next page, select Backup type as Full and Backup all databases. Click Destination to save the Backup to another location. See images below.


![Alt text](image-81.png)


![Alt text](image-82.png)


The Backup of all databases was saved to the D-drive Backup folder destination as per image below.


![Alt text](image-83.png)


Follow the next instruction to complete Backup. Backup of all database to the D-drive Backup folder was successful as per image below.


![Alt text](image-84.png)


![Alt text](image-85.png)


MaintenancePlanFullBackup now in place as per image below in the Object Explorer above.


![Alt text](image-86.png)



## Milestone 5 - Disaster Recovery Simulation



### Task 1 - Mimic Data Loss in the Production Environment.

To mimic data lost in the AdventureWorks2022 database of the Azure SQL Database in the Production Environment (adventure-vm) follow the steps below.

- Open Azure Data Studio in the production environment (adventure-vm) and identify connection to the SQL database (adventure-database)- see image below.

![Alt text](image-89.png)

- Right-click on the adventure-skylight server to select New Query. Select entries in the Sales.PersonCreditCard table and execute it. See image below.


SELECT *
FROM Sales.PersonCreditCard


![Alt text](image-96.png)


- Scroll all the way down the Results pane to determine the number of entries. 19,118 entries were found as per image in the Sales.PersonCreditCard table above. 

- SQL queries were intentionally written to corrupt or delete specific data in the Sales.PersonCreditCard table.


-- Intentional Deletion
DELETE TOP (10000)
FROM Sales.PersonCreditCard


![Alt text](image-97.png)


9,118 entries were left after deletion as per image above.


-- Data Corruption
UPDATE TOP (200) Sales.PersonCreditCard
SET CreditCardID = 146


![Alt text](image-98.png)


![Alt text](image-99.png)


Top 200 CreditCardID were set to 146 due to data corruption as per image below


![Alt text](image-100.png)




### Task 2 - Restore Database from Azure SQL Database Backup

- Access the Azure portal, locate the Azure SQL Database dashboard and select the target database (adventure-database) as per image below.


![Alt text](image-101.png)


- From the SQL Database Home page, the Restore option was selected at the top bar of the page. See image below.


![Alt text](image-102.png)


- A restore database window was opened with a new database name created (adventure-database_2024-01-07T09-08Z). See image below.


![Alt text](image-103.png)


- Click Review + create and finally click Create. See image below.


![Alt text](image-104.png)


New database (adventure-database_2024-01-07T09-08Z) created after deployment. See images below.


![Alt text](image-105.png)


![Alt text](image-106.png)


To verify adventure-database has been restored to a correct point in time before data loss or compromise, run a new query in Azure Data Studio for Select entries in the PersonCreditCard table and execute it.


SELECT *
FROM Sales.PersonCreditCard

Based on different data restoration deployment.

![Alt text](image-107.png)

![Alt text](image-108.png)

![Alt text](image-109.png)


Note: Following the data restoration from Azure portal, only a total of 9,118 entries were restored for Sales.CreditCard table and the CreditCardID column still had 146 set at CreditCardID for the top 200 in the PersonCreditCard table. This was because after execution of the Intentional Deletion and Data Corruption queries, the PersonCreditCard table was saved when closing the query page. Resulting in the earliest point in time data restoration applicable to when the the query was saved. Hence, queries must not be saved when closing query pages after query execution as this could result in a data loss that cannot be restored. Initial data entries for Sales.CreditCard table prior to data loss was 19,118.  However, due to the unfortunate situation that occured, 10,000 entries were lost, resulting in 9,118 entries after data restoration. 

adventure-database(adventure-skylight/adventure-database) was deleted in the Azure portal due to it lacking critical data and suffering data loss. See image below.

![Alt text](image-110.png)

![Alt text](image-111.png)


Following restoration in the Azure portal, the new production environment database is shown below.

![Alt text](image-112.png)




## Milestone 6 - Geo Replication and Failover















































