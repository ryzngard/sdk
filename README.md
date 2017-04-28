Microsoft.NET.Sdk.Web
======================
ASP.NET websdk repo contains the tasks, targets and packages required to build and publish Web Applications.

The websdk repo contains code for the following packages
1. Microsoft.NET.Sdk.Web.ProjectSystem
2. Microsoft.NET.Sdk.Publish &
3. Microsoft.NET.Sdk.Web (Meta-package containing dependency to Microsoft.NET.Sdk.Web.ProjectSystem & Microsoft.NET.Sdk.Publish)

Microsoft.NET.Sdk.Web.ProjectSystem
======================
Project System package defines the following:

- Default globs for the ASP.NET Core Web Projects.
- Project Capabilities for ASP.NET Core Web Projects.

Microsoft.NET.Sdk.Publish
======================
Publish package contains the tasks and targets to publish an ASP.NET core web application.

The following Publish methods are currently supported by the Publish package:
- Folder Publish
- MsDeploy Publish
- MsDeploy Package Publish

Publish CommandLine Usage:

Folder publish:
```
msbuild WebApplication.csproj /p:DeployOnBuild=true /p:PublishUrl="C:\deployedApp\newapp"
or
msbuild WebApplication.csproj /p:DeployOnBuild=true /p:PublishProfile=<FolderProfileName>
or
dotnet publish WebApplication.csproj /p:PublishDir="C:\deployedApp\newapp"
```

MSDeploy Publish:
```
msbuild WebApplication.csproj /p:DeployOnBuild=true /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
or
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployProfileName> /p:Password=<DeploymentPassword>
```

MsDeploy Package Publish:
```
msbuild WebApplication.csproj /p:DeployOnBuild=true /p:PublishProfile=<MsDeployPackageProfileName>
or
dotnet publish WebApplication.csproj /p:PublishProfile=<MsDeployPackageProfileName>
```

Sample EF Migrations section:
```xml
<ItemGroup>
    <DestinationConnectionStrings Include="ShoppingCartConnection">
      <Value>Data Source=tcp:dbserver.database.windows.net,1433;Initial Catalog=shoppingcartdbdb_db;User Id=appUser@dbserver;Password=password</Value>
    </DestinationConnectionStrings>
</ItemGroup>
<ItemGroup>
    <EFMigrations Include="ShoppingCartContext">
      <Value>Data Source=tcp:dbserver.database.windows.net,1433;Initial Catalog=shoppingcartdbdb_db;User Id=efMigrationUser@dbserver;Password=password</Value>
    </EFMigrations>
</ItemGroup>
```
 
Sample Folder Profile:
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <PublishProvider>FileSystem</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <publishUrl>bin\Release\PublishOutput</publishUrl>
    <DeleteExistingFiles>False</DeleteExistingFiles>
  </PropertyGroup>  
</Project>
```

Sample MsDeploy Publish Profile:
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>MSDeploy</WebPublishMethod>
    <PublishProvider>AzureWebSite</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish>http://webappwithdb.azurewebsites.net</SiteUrlToLaunchAfterPublish>
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <MSDeployServiceURL>webappwithdb.scm.azurewebsites.net:443</MSDeployServiceURL>
    <DeployIisAppPath>webappwithdb</DeployIisAppPath>
    <SkipExtraFilesOnServer>True</SkipExtraFilesOnServer>
    <MSDeployPublishMethod>WMSVC</MSDeployPublishMethod>
    <EnableMSDeployBackup>True</EnableMSDeployBackup>
    <UserName>$vramakwebappwithdb</UserName>
    <Password>DeployPassword</Password>
  </PropertyGroup>
</Project>
```
Sample MsDeploy Package Publish Profile
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>Package</WebPublishMethod>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <DesktopBuildPackageLocation>c:\DeployedApp\WebDeployPackage.zip</DesktopBuildPackageLocation>
    <DeployIisAppPath>Default Web Site/WebAppWithDB</DeployIisAppPath>
  </PropertyGroup>
</Project>
```

Sample MsDeploy Profile With Destination Connection String & EF Migrations
```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <WebPublishMethod>MSDeploy</WebPublishMethod>
    <PublishProvider>AzureWebSite</PublishProvider>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <SiteUrlToLaunchAfterPublish>http://webappwithdb.azurewebsites.net</SiteUrlToLaunchAfterPublish>
    <LaunchSiteAfterPublish>True</LaunchSiteAfterPublish>
    <MSDeployServiceURL>webappwithdb.scm.azurewebsites.net:443</MSDeployServiceURL>
    <DeployIisAppPath>webappwithdb</DeployIisAppPath>
    <SkipExtraFilesOnServer>True</SkipExtraFilesOnServer>
    <MSDeployPublishMethod>WMSVC</MSDeployPublishMethod>
    <EnableMSDeployBackup>True</EnableMSDeployBackup>
    <UserName>$vramakwebappwithdb</UserName>
    <Password>DeployPassword</Password>
  </PropertyGroup>
  <ItemGroup>
    <DestinationConnectionStrings Include="ShoppingCartConnection">
      <Value>Data Source=tcp:dbserver.database.windows.net,1433;Initial Catalog=shoppingcartdbdb_db;User Id=appUser@dbserver;Password=password</Value>
    </DestinationConnectionStrings>
  </ItemGroup>
  <ItemGroup>
    <EFMigrations Include="ShoppingCartContext">
      <Value>Data Source=tcp:dbserver.database.windows.net,1433;Initial Catalog=shoppingcartdbdb_db;User Id=efMigrationUser@dbserver;Password=password</Value>
    </EFMigrations>
  </ItemGroup>
</Project>
```

Sample to prevent files from being published:

```xml
<ItemGroup>
    <Content Update="wwwroot/images/*.svg" CopyToPublishDirectory="Never" />
</ItemGroup>
```

Sample to skip specific folders and files during Web Deploy Publish:

```xml
<ItemGroup>
    <MsDeploySkipRules Include="CustomSkipFolder1">
      <ObjectName>dirPath</ObjectName>
      <AbsolutePath>wwwroot</AbsolutePath>
    </MsDeploySkipRules>
	
    <MsDeploySkipRules Include="CustomSkipFolder2">
      <ObjectName>dirPath</ObjectName>
      <AbsolutePath>wwwroot\\Content$</AbsolutePath>
    </MsDeploySkipRules>


    <MsDeploySkipRules Include="CustomSkipFile1">
      <ObjectName>filePath</ObjectName>
      <AbsolutePath>Views\\Home\\About.cshtml</AbsolutePath>
    </MsDeploySkipRules>
    
     <MsDeploySkipRules Include="CustomSkipFile2">
      <ObjectName>filePath</ObjectName>
      <AbsolutePath>Views\\Home\\About2.cshtml</AbsolutePath>
    </MsDeploySkipRules>
</ItemGroup>
```

Pre-Publish and Post-Publish extensibility:

```xml  
  <Target Name="CustomActionsBeforePublish" BeforeTargets="BeforePublish">
    <Message Text="Actions BeforePublish" Importance="high" />
  </Target>
  
  <Target Name="CustomActionsAfterPublish" AfterTargets="AfterPublish">
    <Message Text="Actions AfterPublish" Importance="high" />
  </Target>
```