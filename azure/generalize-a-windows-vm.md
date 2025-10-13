# [Generalize a Windows VM in Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/generalize)

To generalize your Windows VM, follow these steps:
1. Sign in to your Windows VM.
2. Open a Command Prompt window as an administrator.
3. Delete the panther directory (`C:\Windows\Panther`).
4. Verify if CD/DVD-ROM is enabled. If it is disabled, the Windows VM will be stuck at out-of-box experience (OOBE).

```
REM Enable CD/DVD-ROM
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\cdrom /v start /t REG_DWORD /d 1 /f
```


> Verify if any policies applied restricting removable storage access (example: Computer configuration\Administrative Templates\System\Removable Storage Access\All Removable Storage classes: Deny all access)

4. Then change the directory to `%windir%\system32\sysprep`, and then run:

```cmd
sysprep.exe /generalize /shutdown
```

5. The VM will shut down when Sysprep is finished generalizing the VM. Do not restart the VM.
6. Once Sysprep has finished, set the status of the virtual machine to Generalized.
- Open Cloud Shell

```Azure PowerShell
Set-AzVm -ResourceGroupName $rgName -Name $vmName -Generalized
```
