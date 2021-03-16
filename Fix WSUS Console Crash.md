I recently deployed a new WSUS server on Windows Server 2016 but the console would crash, the WSUS engine had crashed and it turns out the problem is it runs out of memory. Make sure your WSUS server had at least 8GB of memory then perform the following:

1.  Open IIS Manager
2.  Select <server> – Application Pools
3.  Right click on WsusPool and select Advanced Settings
4.  Change the Recycling – Private Memory Limit (KB) from 1.4GB to around 4.8GB, e.g. 50331645
5.  Click OK
6.  Start or Recycle the WsusPool

Problem should be fixed!
   

For those still struggling with the issue, and that don’t want to perform a WSUS reinstall, follow the below steps:

To recover your console, run the following in an elevated command prompt (assuming Windows is installed on drive C):

```aws
cd C:\Program Files\Update Services\Tools 
Wsusutil.exe postinstall /servicing 
```
