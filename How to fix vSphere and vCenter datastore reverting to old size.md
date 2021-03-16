# Symptoms:
- You increased the size of a datastore in the past, but now when you open vCenter, you see the old (smaller) size displayed.  There may be low disk space warnings.
- Web client for vCenter 6.5  and vSphere 6.5  and probably vCenter 6.0 and vSphere 6.0
- If you refresh the datastore information, the correct size displays and the warnings go away temporarily.
-The problem re-occurs.

## Root Cause:
According to the VMWare forums, this is caused by having different ESXi versions on the hosts in the datacenter.    Such as one host has Update 1 and another host has Update 3.    The recommended fix is to simply update all ESXi to the same version.

## What happens if you can’t?:
In my case, I needed to use a custom HP image for some servers, and I’m not going to take down the other hosts to install that custom image.   So I kept trying things and found a good workaround.

## Workaround:
For EACH host in the datacenter that had a connection to the faulty storage, I performed these steps:

1. Navigate to Hosts & Clusters tab
2. Select first host
3. Configure tab
4. Storage Devices tab
5. Click button “Refresh host storage info…”
6. Click button “Rescan all storage adapters…”
7. Repeat for next host.
