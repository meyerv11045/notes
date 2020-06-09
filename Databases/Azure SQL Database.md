# Azure SQL Database 
---
Azure SQL Logical Server- an admin container for your databases. Allows control of logins, firewalls, & security policies

DTU (Database Transaction Unit)- simple preconfigured purchase option for compute and storage resources

vCores (Virtual Cores)- more controled purchase option for compute and storage resources

----
### Get info about DB

``` Shell
#Set the Default Name of Resource Group & Logical Server
az configure --defaults group=[group-name]  sql-server=[server-name] 

#List Databases in on your SQL Logical Server
az sql db list 
az sql db list | jq '[.[] | {name: .name}]'

#Get details about specific DB
az qsl db show --name DB-Name | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
```
---
### Connect to DB
```Shell
#Gets the connection string to the specified DB in a format that sqlcmd can use
az sql db show-connection-string --client sqlcmd --name DB-Name
```