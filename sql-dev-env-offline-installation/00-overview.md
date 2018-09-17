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
vs_enterprise.exe --layout X:\VS2017ENT\Packages --lang en-US,zh-CN  --add Microsoft.VisualStudio.Branding.Enterprise --add Microsoft.VisualStudio.MinShell.Resources
```
### SQL Server Data Tools
> File Name: SSDT-Setup-ENU.exe
```command
SSDT-Setup-ENU.exe /layout X:\SSDT2017\Packages
```

## Installation order
1. Install SQL Server Management Studio
2. Install Visual Studio 2017
3. <B>Install Data-Tier Application Framework (DacFx)</B>
4. Install SQL Server Data Tools