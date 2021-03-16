Ubuntu 16.04 LTS provides you the ability to add a user for anyone who plans on accessing your server.  Creating a user is a basic setup but an important and critical one for your server security. In this tutorial, we will create a user and grant administrative access, known as root, to your trusted user.

**Pre-Flight Check**

    1-  Open a terminal and log in as root.
    2-  Work on a Linux Ubuntu 16.04 server.
    
### Creating a User with Root Privileges ###
#### Step 1:  Add The User ####

Create a username for your new user, in my example my new user is user1:

```adduser user1```

You’ll then be prompted to enter a password for this user.   We recommend using a strong password because malicious bots are programmed to guess simple passwords. If you need a secure password, this third party password generator can assist with creating one.

**Output:**

```aws~# adduser user1
Adding user 'user1' ...
Adding new group 'user1' (1002) ...
Adding new user 'user1' (1002) with group `' ...
Creating home directory '/home/user1' ...
Copying files from '/etc/skel' ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Prompts will appear to enter in information on your new user.  Entering this information is not required and can be skipped by pressing enter in each field.
```aws
Enter the new value or press ENTER for the default
Full Name []:
Room Number []:
Work Phone []:
Home Phone []:
Other []:
```

Lastly, the system will ask you to review the information for accuracy.  Enter Y to continue to our next step.

```Is the information correct? [Y/n]```

**Step 2: Grant Root Privileges**

Assigning a user root access is to grant a user the highest power.  My user, user1, can then make changes to the system as a whole, so it’s critical to allow this access only to users who need it. Afterward, user1 will be able to use sudo before commands that are usually designed to be used by the root user.

```usermod -aG sudo user1```

**Step 3: Verify New User**

As root, you can switch to your new user with the su – command and then test to see if your new user has root privileges.

```su - user1```

If the user has properly been granted root access the command below will show user1 in the list.

```grep '^sudo' /etc/group```

Output:

```sudo:x:27:user1```
