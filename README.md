# Creating an Azure SQL Database 

Azure SQL Database is a popular option for storing and managing data. This article explains step by step how to create Azure SQL Database.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/c591271a-1a85-477a-9a7f-edf50fc16848)

**Türkçe Kaynak**: https://medium.com/@ayigit/azure-sql-veritaban%C4%B1-olu%C5%9Fturma-4d84495f837

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/ab6fd591-9774-4dfa-8297-3249396bf375)

In the first step, a SQL script is prepared to create a new database. This script specifies the name of the database. However, instead of physically creating the mdf and ldf files in the C folder, it is intended to create a file on Azure. A new script needs to be created by specifying the name of the database.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/d2236708-84d1-479b-92d3-3757eb9c6299)

**Azure Storage Explorer**

Through Azure Storage Explorer, the container on Azure Explorer is accessed and the container's URL information is obtained.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/10452ff4-81d9-4cae-b22e-f1b1dd377614)

This URL is pasted where the source is specified to be used in the SQL.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/e0e2ea4e-91b8-4a69-beb1-005b546c4e80)

To get the key, right-click the container in the Storage Explorer tool and select Manage Access Policies to get the signature.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/c386c928-c0c9-4aa9-9844-adcf6a09aaaa)

After choosing the name of the access and what the authorizations will be, the recording stage is started.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/9735259e-f92b-471e-841d-f7ef22950ae4)

You need to create a special signature for the created policy. For this, right-click on the container again and select get shared access signature.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/bdb065cc-f74c-40c9-aff1-cd52d5a6f3f4)

Take the part up to the question mark (?) in the URL. You can see the part after the question mark in the Query string field. You will also use this field as a password.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/d6049501-e376-4500-8297-d981582cf16e)

If you want to access any object inside SQL Server, you need to use login and user.
If we want to access outside from SQL Server, Crenditals comes into play.
Right-click in the Credentials section of the Security section of SQL and create a new credential by saying new credential.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/dce033ad-a48c-404d-bb77-3db3c71f40b3)

Credential's name is the URL field used in the previous steps.
Identity: SHARED ACCESS SIGNATURE (This field needs to be defined because Shared Access Signature is used.)
In the Password field, copy and paste the part after the question mark we mentioned above.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/5ec5e598-55cd-47db-8738-0380849a9c99)

Then run the relevant script.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/03a8eb55-918f-4432-8bab-d9294cf6790f)

Mdf and Ldf files were created in the cloud.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/ecde49eb-f16f-43d6-8815-a150d9211eb2)

**Backup**

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/58b50007-4202-4428-b60e-9db8be19b976)

If you select the URL back up to option in the Destination field, you can backup Azure disks.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/7d76ced8-48d5-4998-a4f0-bcc153af3ace)

Define our container and complete the process.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/c6b65712-656e-4d56-aa02-46782b1b706b)

**Backup Options**

If you select Compress backup in the Compression field, you can get a faster backup.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/e1e3e6dd-e334-464f-aa2a-4c025e98956b)

**Azure Explorer Backup**

You can also see the backups taken in the cloud environment.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/598c0531-14e5-474c-b7da-995da9ecbabe)

As a result, Azure SQL Database creation and backup are important steps for data management. In this article, the steps to create a database on Azure are explained in detail. While database files are created in the cloud via Azure Storage Explorer, backups can be easily performed with Backup options. These steps allow users to effectively and securely perform database management on the Azure platform.
