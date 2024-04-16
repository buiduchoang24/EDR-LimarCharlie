# SOC-Analyst

## Set up VMs environment
- I set up 2 VMs, one is Ubuntu Server 22.04, the other is Windows 10 Desktop
- After setting up completely, I install sysmon in Windows 10 VM by this following Powershell script steps
1. Download Sysmon
```powershell
Invoke-WebRequest -Uri https://download.sysinternals.com/files/Sysmon.zip -OutFile C:\Windows\Temp\Sysmon.zip
```
2. Unzip Sysmon.zip
```powershell
Expand-Archive -LiteralPath C:\Windows\Temp\Sysmon.zip -DestinationPath C:\Windows\Temp\Sysmon
```


