
Here some tables with authentication error code for quick understand what’s happpen

| **NETLOGON LOG ERROR CODE** |	**DESCRIPTION** |
| -------------- | --- |
| 0x0	| Successful login |
| 0xC0000064	| The specified user does not exist
| 0xC000006A	| The value provided as the current password is not correct
| 0xC000006C	| Password policy not met
| 0xC000006D	| The attempted logon is invalid due to a bad user name
| 0xC000006E	| User account restriction has prevented successful login
| 0xC000006F	| The user account has time restrictions and may not be logged onto at this time
| 0xC0000070	| The user is restricted and may not log on from the source workstation
| 0xC0000071	| The user account’s password has expired
| 0xC0000072	| The user account is currently disabled
| 0xC000009A	|Insufficient system resources
| 0xC0000193	| The user’s account has expired
| 0xC0000224	| User must change his password before he logs on the first time
| 0xC0000234	| The user account has been automatically locked


| **LOGON EVENT ID** | **DESCRIPTION** |
| --------- | --- |
| 528	| A user successfully logged on to a computer. For information about the type of logon, see the Logon Types table below.
| 529	| Logon failure. A logon attempt was made with an unknown user name or a known user name with a bad password.
| 530	| Logon failure. A logon attempt was made, but the user account tried to log on outside of the allowed time.
| 531	| Logon failure. A logon attempt was made using a disabled account.
| 532	| Logon failure. A logon attempt was made using an expired account.
| 533	| Logon failure. A logon attempt was made by a user who is not allowed to log on at this computer.
| 534	| Logon failure. The user attempted to log on with a type that is not allowed.
| 535	| Logon failure. The password for the specified account has expired.
| 536	| Logon failure. The Netlogon service is not active.
| 537	| Logon failure. The logon attempt failed for other reasons. Note: In some cases, the reason for the logon failure may not be known.
| 538	| The logoff process was completed for a user.
| 539	| Logon failure. The account was locked out at the time the logon attempt was made.
| 540	| A user successfully logged on to a network.
| 541	| Main mode Internet Key Exchange (IKE) authentication was completed between the local computer and the listed peer identity (establishing a security association), or quick mode has established a data channel.
| 542	| A data channel was terminated.
| 543	| Main mode was terminated. Note: This might occur as a result of the time limit on the security association expiring, policy changes, or peer termination. (The default expiration time for security associations is eight hours.)
| 544	| Main mode authentication failed because the peer did not provide a valid certificate or the signature was not validated.
| 545	| Main mode authentication failed because of a Kerberos failure or a password that is not valid.
| 546	| IKE security association establishment failed because the peer sent a proposal that is not valid. A packet was received that contained data that is not valid.
| 547	| A failure occurred during an IKE handshake.
| 548	| Logon failure. The security identifier (SID) from a trusted domain does not match the account domain SID of the client.
| 549	| Logon failure. All SIDs that correspond to untrusted namespaces were filtered out during an authentication across forests.
| 550	| A denial-of-service attack may have taken place.
| 551	| A user initiated the logoff process.
| 552	| A user successfully logged on to a computer using explicit credentials while already logged on as a different user.
| 672	| An authentication service (AS) ticket was successfully issued and validated.
| 673	| A ticket-granting service (TGS) ticket was granted.
| 674	| A security principal renewed an AS ticket or TGS ticket.
| 675	| Preauthentication failed. This event is generated on a Key Distribution Center (KDC) when a user types in an incorrect password.
| 676	| Authentication ticket request failed. This event is not generated in Windows XP or in the Windows Server 2003 family.
| 677	| A TGS ticket was not granted. This event is not generated in Windows XP or in the Windows Server 2003 family.
| 678	| An account was successfully mapped to a domain account.
| 681	| Logon failure. A domain account logon was attempted. This event is not generated in Windows XP or in the Windows Server 2003 family.
| 682	| A user has reconnected to a disconnected terminal server session.
| 683	| A user disconnected a terminal server session without logging off. Note: This event is generated when a user is connected to a terminal server session over the network. It appears on the terminal server.

| **Event ID Field**	| **Comments** | 
| --- | --- |
| Event Type, Source,Category,ID,Date,and Time	| self-explanatory | 
| User	| The user account performing the logon. For example, this might be NT AUTHORITYSYSTEM,which is the LocalSystem account used to start many Windows 2000 services.
| Computer	| The computer on which the event occurred
| Reason	| Applies to logon failures only; it’s the reason the account failed to log on.
| User Name	| The name of the user account attempting to log on
| Domain	| The domain of the user account attempting to log on.
| Logon Type	| A numeric value indicating the type of logon attempted. Possible values are: 
- Interactive (interactively logged on)
- Network (accessed system via network)
- Batch (started as a batch job)
– Service (a Windows service started by service controller)
– Proxy (proxy logon; not used in Windows NT or Windows 2000)
– Unlock (unlock workstation)
– NetworkCleartext (network logon with cleartext credentials)
– NewCredentials (used by RunAs when the /netonly option is used) 
| Logon Process	| The process performing the logon. The following are some example logon processes:
– Advapi (triggered by a call to LogonUser; LogonUser calls LsaLogonUser, and one of the arguments to LsaLogonUser, OriginName, identifies the origin of the logon attempt)
– User32 (normal Windows 2000 logon using WinLogon)
– SCMgr (Service Control Manager started a service)
– KsecDD (network connections to the SMB server-for example, when you use a NET USE command)
– Kerberos (the Kerberos Security Support Provider [SSP])
– NtlmSsp (the NTLM SSP)
– Seclogon (Secondary Logon-that is, the RunAs command)
– IIS (IIS performed the logon; generated when logging on the IUSR_machinename account or when using Digest or Basic authentication)
| Authentication Package	| The security package called to attempt to log on the account. An authentication package is a dynamic-link library (DLL) that analyzes logon data and determines whether to authenticate an account. Most common examples are Kerberos, Negotiate, NTLM, and MICROSOFT_AUTHENTICATION_PACKAGE_V1_0 (also called MSV1_0; authenticates users in the SAM database, supports pass-through authentication to accounts in trusted domains, and supports subauthentication packages) Workstation Name Workstation name, if known, used by the principal during logon.|
