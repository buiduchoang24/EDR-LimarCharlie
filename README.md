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

- I use LimaCharlie (a SecOps cloud platform)
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/bdce3c63-38eb-42a6-81f6-626cfc5138e1)
- Follow these steps, and I reach this. It successfully creates the sensor
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/a9985c93-978d-4c3a-83d8-5d23d9e3f49b)



