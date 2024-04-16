# SOC-Analyst

## Set up VMs environment
- I set up 2 VMs, one is Ubuntu Server 22.04, the other is Windows 10 Desktop
- After setting up completely, I install sysmon in Windows 10 VM by this Powershell script
```powershell
Invoke-WebRequest -Uri https://download.sysinternals.com/files/Sysmon.zip -OutFile C:\Windows\Temp\Sysmon.zip
```


