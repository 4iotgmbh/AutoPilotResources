# AutoPilotResources

## Steps

Snippets to get zero touch Autopilot going

- start from clean windows image
- inject drivers
- register Autopilot HW hash

## Setup Tasks

- Setup OSDCloud environment
- replace the following replacement strings:
  - {Entra-TenantID}
  - {Entra-AppID}
  - {Entra-AppSecret}
- check / replace time server and timezone variables

```Powershell
$StartPSCommand = @'
    [Environment]::SetEnvironmentVariable('OSDCloudAPTenantID','{Entra-TenantID}','Machine'); [Environment]::SetEnvironmentVariable('OSDCloudAPAppID','{Entra-AppID}','Machine'); [Environment]::SetEnvironmentVariable('OSDCloudAPAppSecret','{Entra-AppSecret}','Machine')
'@
$Params = @{
 CloudDriver = 'Dell','USB'
 StartOSDCloudGUI = $False
 DriverPath = 'C:\DRIVERS'
 StartPSCommand = $StartPSCommand
 StartURL = 'https://raw.githubusercontent.com/4iotgmbh/AutoPilotResources/main/ZTI.ps1'
}
Edit-OSDCloudWinPE @Params
```

See ZTI.ps1 in repo.

## References

- <https://www.bsi.bund.de/SharedDocs/Downloads/DE/BSI/Cyber-Sicherheit/SiSyPHus/Workpackage5_TPM-Nutzung_V1_1.pdf?__blob=publicationFile&v=2>
- <https://www.reddit.com/r/PowerShell/comments/1ak9uu2/comment/kpavfkj/>
- <https://github.com/mmeierm/Scripts/tree/main/Autopilot>
- <https://mikemdm.de/2023/01/29/can-you-create-a-autopilot-hash-from-winpe-yes/>
- <https://www.reddit.com/r/Intune/comments/1456ezw/osdcloud_offlineonline_device_provisioning_and/>
- <https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/oa3-command-line-config-file-syntax?view=windows-11>
