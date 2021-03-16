> If you want a more thorough view of how much space the SxS folder is taking up and the option to clean up unneeded files, use the Command Prompt.


1. **Launch the command prompt with admin privileges**. You can do this by right-clicking on the Windows icon in the taskbar and click “Command Prompt (Admin).” or by just typing cmd on the start menu and then selecting Run as Administrator

![image](https://user-images.githubusercontent.com/67142634/111326485-7ef88580-8664-11eb-963d-c4c1f53d656a.png)

2. Enter the command: 
```aws
Dism.exe /online /Cleanup-Image /StartComponentCleanup
```
![image](https://user-images.githubusercontent.com/67142634/111326551-8cae0b00-8664-11eb-8334-b66209d534de.png)

It could take a few minutes for the DISM tool to analyze the folder. When it’s done, you’ll see size details of the components in the WinSxS folder and, at the bottom, a recommendation to clean it up or not.

3. If required, clean up the folder using this command in the Command Prompt: 
```aws
Dism.exe /online /Cleanup-Image /StartComponentCleanup
```

There’s another command you can use to uninstall Windows updates and service packs, which saves more space, but we don’t recommend you do that, because you won’t be able to uninstall any current service updates or service packs after performing this. The command is 

```aws
Dism.exe /online /Cleanup-Image /StartComponentCleanup
```
The cleanup might take some time, depending on your system and how much you’re deleting, but that extra space will be worth it.
