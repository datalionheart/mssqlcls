# SQL Server Development Environment Offline Installation
## Software requirements
| ID | Item | Remark | Download | Size |
| --- | --- | --- | --- | --- |
| 1 | Visual Studio 2017 | Online | [Download](https://visualstudio.microsoft.com/downloads/)| 1.2MB |
| 2 | SQL Server Data Tools | Online | [Download](https://go.microsoft.com/fwlink/?linkid=2014060)| 1.5MB |
| 3 | Data-Tier Application Framework (DacFx) | Full package | [Download](https://www.microsoft.com/en-us/download/details.aspx?id=56508)|  5.5MB |
| 4 | SQL Server Management Studio | Full package | [Download](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)| 807MB |
> P.S. Must be match Windows Server Language

## Get offline installation packages
### Visual Studio 2017
> File Name: vs_enterprise.exe
```command
vs_enterprise.exe --layout X:\VS2017ENT\Packages --lang en-US zh-CN
```
Show:
-- Download Visual Studio Online Installer
![](./pictures/VS2017Download01.png)
-- Startup Visual Studio Online Installer by Command Lines
![](./pictures/VS2017Download02.png)
-- Maybe need waiting few hours by your network bandwidth
![](./pictures/VS2017Download03.png)
-- Download complete
![](./pictures/VS2017Download04.png)
-- Full package size over 42 GB
![](./pictures/VS2017Download05.png)
> P.S. <br/>
* First time download or offline packages update with the same script
* [Create an offline installation of Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/create-an-offline-installation-of-visual-studio?view=vs-2017)
* [List of language locales](https://docs.microsoft.com/en-us/visualstudio/install/create-an-offline-installation-of-visual-studio?view=vs-2017#list-of-language-locales)<br/>
![Language Locales](./pictures/language-locales.png)


### SQL Server Data Tools
> File Name: SSDT-Setup-ENU.exe
```command
SSDT-Setup-ENU.exe /layout X:\SSDT2017\Packages
```
-- Startup SSDT Online Installer begin for download
![](./pictures/SSDT2017Download01.png)
-- Download complete
![](./pictures/SSDT2017Download02.png)
> P.S. First time download or offline packages update with the same script

## Create Share Folder
```powershell
// Powershell Run as Administrator
New-SmbShare -Name "VS2017ENT" -Path "X:\VS2017ENT\Packages" -ReadAccess "Everyone"
New-SmbShare -Name "SSDT2017" -Path "X:\SSDT2017\Packages" -ReadAccess "Everyone"
```
> P.S.<br/>
Share Visual Studio Packages Floder<br/>
![](./pictures/VS2017PackageShare01.png)
Share SQL Server Data Tools Packages Floder<br/>
![](./pictures/SSDT2017PackageShare01.png)

## Installation order
1. Install SQL Server Management Studio

2. Install Visual Studio 2017
Open shared folder
![](./pictures/VS2017OfflineInstall01.png)
Enter access user name and password
> P.S.<br/>
If do not choose checkbox remember login information
![](./pictures/VS2017OfflineInstall02.png)
Find and execute vs_setup.exe
![](./pictures/VS2017OfflineInstall03.png)
Review and continue agreement
![](./pictures/VS2017OfflineInstall04.png)
Failure！Can not be access local or remote files
![](./pictures/VS2017OfflineInstall05.png)
![](./pictures/VS2017OfflineInstall06.png)
Enter access user name and password
> P.S.<br/>
Choose checkbox remember login information
![](./pictures/VS2017OfflineInstall07.png)
Installer finded need files
![](./pictures/VS2017OfflineInstall08.png)
Installer download and install file from shared folder
![](./pictures/VS2017OfflineInstall09.png)
Choose Data Storage and Processing for install SSDT shell
![](./pictures/VS2017OfflineInstall10.png)
Wating for download and install complete
![](./pictures/VS2017OfflineInstall11.png)
Visual Studio 2017 offline install completed
![](./pictures/VS2017OfflineInstall12.png)
Initial Visual Studio 2017 and Close
![](./pictures/VSInit01.png)
![](./pictures/VSInit02.png)
![](./pictures/VSInit03.png)

3. <B>Install Data-Tier Application Framework (DacFx)</B>
![](./pictures/InstallDacFx01.png)
![](./pictures/InstallDacFx02.png)
![](./pictures/InstallDacFx03.png)
![](./pictures/InstallDacFx04.png)

4. Install SQL Server Data Tools
Open Shared Folder find SSDT offline package files
![](./pictures/InstallSSDT01.png)
Execute SSDT offline install file
![](./pictures/InstallSSDT02.png)
Click Next for continue
![](./pictures/InstallSSDT03.png)
Choose Visual Studio 2017 XX Edition and choose components every you want then begin install
![](./pictures/InstallSSDT04.png)
Download files from remote shared folder for install
![](./pictures/InstallSSDT05.png)
SSDT Offline install complete
![](./pictures/InstallSSDT06.png)