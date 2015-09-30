#Magic Books
##About
This app searches for books from a database based on their ISBN. It's designed to illustrate a performance problem which can be experienced when accessing data from SQL Server with Entity Framework, without paying proper attention to SQL Server data types.
##Setup
1) Create a new blank database in SQL Server called `MagicBooks`.

2) Create the database schema by running the following script:

```
CREATE TABLE [dbo].[Books]
(
[BookId] [int] NOT NULL IDENTITY(1, 1),
[ISBN] [varchar] (20) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Title] [nvarchar] (100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Author] [nvarchar] (100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
[Copies] [int] NOT NULL,
[Large] [bit] NOT NULL,
[PublishDate] [date] NOT NULL
) ON [PRIMARY]

CREATE NONCLUSTERED INDEX [NonClusteredIndex_Isbn] ON [dbo].[Books] ([ISBN], [BookId])
INCLUDE ([Author], [Copies], [Large], [PublishDate], [Title]) ON [PRIMARY]
```

3) Add some data to the table. This is most easily achieved by running the /Database/SampleDataGeneration.sqlgen file with Redgate's [Sql Data Generator](http://www.red-gate.com/products/sql-development/sql-data-generator/), but you can use another technique to generate some realistic test data if you prefer.

4) Open /Application/BookSearch.sln in Visual Studio. Modify the connection string in App.Config to point to the correct database.

5) Build the appliction.
