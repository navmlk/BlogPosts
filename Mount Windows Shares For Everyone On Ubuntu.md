This post is going to show you how to automatically mount the Windows shared folder on Ubuntu machines for everyone to access. No passwords needed and everyone body will be able to create, modify and delete files and folders from there shared location.

This setup is is great for environments where you want users to temporarily store content before moving to a more secure location. You don’t want your users storing content for long here since everyone has full rights to create, delete and modify files and folders

To mount Windows shares on Ubuntu automatically, follow the steps below:

### Step 1: Create Windows Shares ###
This first step mounting Windows shares on Ubuntu is to create a Windows share.

### Step 2: Install CIFS or SMBFS ###
Now that you’ve created a Windows share with everyone having full access, run the commands below to install smbfs or cifs package on Ubuntu.

```aws 
sudo apt-get install cifs-utils
```

After installing, continue below to create a location to mount the Windows shares.

### Step 3: Create a Mount Point ###
After installing the Ubuntu packages that allows for sharing between two systems, run the commands below to create a location to mount the Windows share. This location will be linked to the Windows share on Ubuntu with everyone having full access.

The folder we’ll want to create for the Windows share will be called winshare.

```aws
sudo mkdir /media/winshare
```

Next, run the commands below on the mount point to give everyone access
```aws
sudo chown -R nobody:nogroup /media/winshare
sudo chmod -R 0777 /media/winshare
```

### Step 4: Mount the Windows Share ###

Now that all the requirements are met, run the commands below to open Linux fstab file.

```aws
sudo nano /etc/fstab
```

Then add the line below into the file and save.

```aws
//WINDOWSPC/PublicShares /media/winshare cifs username=winuser,password=winuserpasswd,uid=nobody,iocharset=utf8,noperm 0 0
```

Save the file and you’re done.

The line details:

-   **username and password** indicates a windows user account and password to access the shared folder.
-   **uid=nobody** makes the Linux user specified by the id the owner of the mounted share, allowing anyone access.
-   **iocharset=utf8** allows access to files with names in non-English languages.

Now all you have to do to mount the file is run the commands below:
```aws
sudo mount -a
```

If you’re using Ubuntu desktop, browse to the mount directory and the Windows share should be mounted there.

If  get an error, restart the computer.
