#
Create a Storage Account.
Create a SQL Server and db.
Create an appinsight and get the instrumentation key.
Create a KeyVault in Azure and Specify 4 secrets.
ApplicationInsights--InstrumentationKey
ConnectionStrings--SportsStoreConnection
StorageAccountInformation--StorageAccountAccessKey
StorageAccountInformation--StorageAccountName

Once done, publish this application inside an app service. Go to Identity and assign System defined identity to it. Note down the object id. Also add ASPNETCORE_ENVIRONMENT config setting.
Go to Keyvault--Access Policy
Give Secrete management and Get/List permissions for it. and save.

# SSMVCCoreApp (.Net Core 2.2.402)

#### Packages

* Nuget Packages for the Project
  * For Azure Storage
    1. Install-Package WindowsAzure.Storage -Version 9.3.3 or Latest
  * For Azure Application Insights
      1. Install-Package Microsoft.ApplicationInsights.AspNetCore -Version 2.7.1 or (latest)
      2. Install-Package Microsoft.Extensions.Logging.ApplicationInsights -Version 2.10.0 (for logging ILogger user defined logs in ApplicationInsights)
  * For Azure Key Vault
        Install-Package Microsoft.Azure.KeyVault -version 3.0.5
        Install-Package Microsoft.Azure.Services.AppAuthentication -version 1.5.0
        Install-Package Microsoft.Extensions.Configuration.AzureKeyVault -version 2.2.0
  * For Redis Cache
        Install-Package Microsoft.Extensions.Caching.Redis -version 2.2.0
#### Bower  

* Bower Packages for the Project
  1. jquery - 3.4.1
  2. bootstrap - 4.2.1
  3. font-awesome - 4.7.0
  4. jquery-validation - 1.19.1
  5. jquery-validation-unobtrusive - 3.2.11


#### Entity Framework Core Commands
    
1. Create the Entities with the Annotations, DbContext class
2. Add ConnectionStrings to the appsettings.json file
3. Add the service.AddDbContext and pass the connectionString to it and also set the Resilient Entity Framework Core SQL connections (Similar to SqlAzureExecutionStrategy in MVC5)
4. In the CMD  (dotnet tool install --global dotnet-ef this will install the dotnet-ef cli)
  4.1 dotnet ef database update (This will create the database)  
  4.2 dotnet ef migrations add InitialDB -o DataMigrations\Migrations (This will create the class with the table schema)  
  4.3 dotnet ef migrations remove (This will remove the migrations)  
  4.4 dotnet ef database update (This will create the database, if the database exits then it will update the database with the latest changes)  
  4.5 dotnet ef database drop (This will drop the database)

```sql
CREATE TABLE [dbo].[Products] (
    [ProductId]   INT             IDENTITY (1, 1) NOT NULL,
    [ProductName] NVARCHAR (100)  NOT NULL,
    [Description] NVARCHAR (250)  NOT NULL,
    [Price]       DECIMAL (18, 2) NOT NULL,
    [Category]    NVARCHAR (100)  NOT NULL,
    [PhotoUrl]    NVARCHAR (MAX)  NULL
);

Select * from Products
```