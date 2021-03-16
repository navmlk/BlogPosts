If you’re a **SQL Server Pro** you will know that the volumes the SQL log and datafiles are stored on should be formatted with a **64K cluster size**. This is a SQL Server Best practice as stated in [this](https://technet.microsoft.com/en-us/library/dd758814(v=sql.100).aspx) link.

I found [this](http://stuart-moore.com/get-cluster-size-disks-volumes-windows-machine-using-powershell-wmi/) handy piece of PowerShell code that gets just the allocation unit size for all disks in the system:
```aws
$sql = "SELECT Label, Blocksize, Name FROM Win32_Volume WHERE FileSystem='NTFS'"  
Get-WmiObject -Query $sql -ComputerName '.' | Select-Object Label, Blocksize, Name 
```
The result of which would look similar to this on a system running SQL Server:
![image](https://user-images.githubusercontent.com/67142634/111341071-149a1200-8671-11eb-80af-efce18745a0a.png)

The results above show which disks are configured with the default 4K allocation unit size and those configured with 64K which are the SQL disks.
