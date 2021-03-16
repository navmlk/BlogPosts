When you turn on periodic time synchronization, VMware Tools sets the time of the guest operating system to be the same as the time of the host.

After time synchronization occurs, VMware Tools checks once every minute to determine whether the clocks on the guest and host operating systems still match. If not, the clock on the guest operating system is synchronized to match the clock on the host.

If the clock on the guest operating system falls behind the clock on the host, VMware Tools moves the clock on the guest forward to match the clock on the host. If the clock on the guest operating system is ahead of that on the host, VMware Tools causes the clock on the guest to run more slowly until the clocks are synchronized.

Native time synchronization software, such as Network Time Protocol (NTP) for Linux and the Mac OS X, or Microsoft Windows Time Service (Win32Time) for Windows, is typically more accurate than VMware Tools periodic time synchronization and is therefore preferred. Use only one form of periodic time synchronization in your guests. If you are using native time synchronization software, turn off VMware Tools periodic time synchronization.

Regardless of whether you turn on VMware Tools periodic time synchronization, time synchronization occurs after certain operations:

-   When the VMware Tools daemon is started (such as during a reboot or power on operation)
-   When resuming a virtual machine from a suspend operation
-   After reverting to a snapshot
-   After shrinking a disk
When the operating system starts or reboots, and when you first turn on periodic time synchronization, synchronization can be either forward or backward in time. For other events, synchronization is forward in time.

To disable time synchronization completely, you must edit the configuration file (.vmx file) of the virtual machine and set several synchronization properties to FALSE.Prerequisites

-   Disable other periodic time synchronization mechanisms. For example, some guests might have NTP or Win32Time clock synchronization turned on by default.
-   If you plan to script the commands used in this procedure and need to know what the exit codes are, see Exit Codes.

Note

Mac OS X guests use NTP and do not become out of sync with the host. For Mac OS X guests, there is no need to turn on VMware Tools time synchronization.Procedure

1.  Open a command prompt or terminal in the guest operating system.
2.  Change to the VMware Tools installation directory.Operating SystemDefault PathWindowsC:\Program Files\VMware\VMware ToolsLinux and Solaris/usr/sbinFreeBSD/usr/local/sbin
3.  Enter the command to determine whether time synchronization is enabled.utility-name timesync status For utility-name use the guest-specific program name.Operating SystemProgram NameWindowsVMwareToolboxCmd.exeLinux, Solaris, and FreeBSDvmware-toolbox-cmd
4.  Enter the command to enable or disable periodic time synchronization.utility-name timesync subcommand For subcommand, use enable or disable.

After you complete this procedure, the VMware Tools service enables or disables periodic time synchronization, as you specified. Disabling periodic time synchronization does not disable all VMware Tools time synchronization.

Reference: https://pubs.vmware.com/vsphere-50/index.jsp?topic=%2Fcom.vmware.vmtools.install.doc%2FGUID-C0D8326A-B6E7-4E61-8470-6C173FDDF656.html
