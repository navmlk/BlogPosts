The **NetworkManager** text user interface (TUI) tool, **nmtui,** provides a text interface to configure networking by controlling **NetworkManager**. The tool is contained in the _NetworkManager-tui_ package. At time of writing, it is not installed along with **NetworkManager** by default. To install _NetworkManager-tui_, issue the following command as _root_:

```aws
~]# yum install NetworkManager-tui
```
If required, for details on how to verify that **NetworkManager** is running, see [Section 1.4.1, “The NetworkManager Daemon”](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-Installing_NetworkManager.html#sec-The_NetworkManager_Daemon).To start **nmtui**, issue a command as follows:

```aws
~]$ nmtui
```
The text user interface appears. To navigate, use the arrow keys or press **Tab** to step forwards and press **Shift+Tab** to step back through the options. Press **Enter** to select an option. The **Space** bar toggles the status of a check box.The following commands are available:

-   _nmtui edit connection-nameIf_ no connection name is supplied, the selection menu appears. If the connection name is supplied and correctly identified, the relevant **Edit connection** screen appears.
-   _nmtui connect connection-nameIf_ no connection name is supplied, the selection menu appears. If the connection name is supplied and correctly identified, the relevant connection is activated. Any invalid command prints a usage message.

At time of writing, **nmtui** does not support all types of connections. In particular, you cannot edit VPNs, wireless network connections using WPA Enterprise, or Ethernet connections using _802.1X_.

Reference: https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-Networking_Config_Using_nmtui.html
