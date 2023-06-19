# Easy Way to Bulk Copy Table Data: BCP Copy Utility

BCP Copy Utility is a utility for batch copying data between a Microsoft SQL Server instance and a data file in a user-specified format. This utility can be used to import large numbers of new rows into SQL Server tables or to export data from tables to data files. No Transact-SQL knowledge required, except when used with the query option.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/30a93967-4f59-494b-92e3-a45fc9218e4e)

**Türkçe Kaynak:** https://medium.com/@ayigit/tablo-verilerini-toplu-olarak-kopyalaman%C4%B1n-kolay-yolu-bcp-copy-utility-52245114183e

BCP Copy Utility, bir tabloya veri aktarmak için o tablo için oluşturulmuş bir format dosyası kullanmanızı veya tablonun yapısını ve sütunları için geçerli olan veri türlerini anlamanızı gerektirir. Bu nedenle, öncelikle verileri aktarmak istediğiniz tabloyu ve tablodaki sütunları anlamalısınız.Aşağıdaki linkten indirebilirsiniz.

https://docs.microsoft.com/en-us/sql/tools/bcp-utility?view=sql-server-ver16  

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/f854d294-2dce-41bc-86c1-198442b1cdc7)

Where is it located? (cmd>Where bcp)

C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn\bcp.exe

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/bec63c8e-a7ee-4955-bbb3-98e9455cbcc9)

We can see a database called SourceDB and 2 tables in the image below.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/4074cd5c-44b7-4899-baca-222ba98c60c7)

Our goal is to export the contents of the Sales table. So I am Truncate the Exports table.

This data is not intended to be exported to the Exports table. Therefore, it is not desirable to affect the data in the Exports table from the Sales table. Therefore, the contents of the Exports table are cleared beforehand with the "TRUNCATE" operation. The "TRUNCATE" operation deletes all data in the table and preserves the structural integrity of the table. After this process, the Exports table becomes empty and there is no conflict during the data copying process from the Sales table.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/d52e5cf6-fc63-4018-a5f1-1d34780a9ae5)

BCP Copy Utility can be run with parameters "-c" and "-n". The "-c" parameter is used to get a readable output, while the "-n" parameter is used to get native output.

**bcp SourceDB.dbo.Sales out C:\Data\Sales.csv -c -t, -S localhost -T**

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/9b0f0e97-4f53-417f-bfbd-ca4bc3fccc20)

We can see that it has made a copy of 4 rows in the Sales table. When we go to the bottom of the Data File, we can see that our Sales table has been copied.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/b334a64d-bc2a-49e0-be27-85d46c0ea08c)

**Sales Table**

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/1979befd-de88-4c69-a75c-7178043fe7d9)

In the first operation, we kept the data in single row and single column and it was not very useful.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/eec47240-7d45-49c0-89d6-8bc93f57ab7f)

If we want to see it as a normal table, we need to create a format file.
For this process, we need to run the following command in cmd.

**bcp SourceDB.dbo.Sales format nul -f C:\Data\Sales.fmt -c -t, -S localhost -T**

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/82623048-a95f-444d-8663-1c0e4604626c)

We can see the format file we created under our data file.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/c215103f-f74f-4766-9c81-a42b7a226253)

We can access information such as which column and type from the created file.
When using the bcp utility to add data to the table, you must specify a complete list of columns into which the data will be inserted into the table. You must also specify the correct data types for the columns. This is important to ensure correct data transfer and to avoid any data type incompatibility or format errors.

The bcp utility provides support for many different data types, for example varchar, int, datetime and numeric etc. The data type must be compatible with the columns in the data file for the data to be transferred correctly.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/7e4e2c57-da3a-47d8-bbf0-5f2f72a3f640)

After exporting the data to a CSV file, you can export this file to the SQL Server database via a view. You can do this using the "OPENROWSET" function.
For example, if you want to view the data in the "Sales" table through a view, you can use the following command:
We can read the content in the format separated by columns through the format file created in SQL.

![image](https://github.com/aysegulyigitbi/SQL/assets/127193220/7b7e5d21-f12c-4ba1-b817-25136992d1d1)

**We can create a web and read the external csv continuously.**

--single line, single column
SELECT *
FROM OPENROWSET (
BULK 'C:\Data\Sales.csv',
SINGLE_CLOB
        ) AS t1;


--In a columnar format
SELECT *
FROM OPENROWSET (
BULK 'C:\Data\Sales.csv',
FORMATFILE='C:\Data\Sales.fmt'
        ) AS t1;

The bcp utility also allows you to copy data from a specific range of a data file or table.

The bcp utility can be used to import data files into SQL Server as well as importing data from many data sources to SQL Server. For example, you can export data contained in a data file to a SQL Server table, or you can export data from a SQL Server table to a data file.

All in all, the bcp utility provides a quick and easy way to export large amounts of data to SQL Server. This utility is versatile and can import data from many different data sources or data files. It also provides the data type and column information needed to correctly transfer data.
