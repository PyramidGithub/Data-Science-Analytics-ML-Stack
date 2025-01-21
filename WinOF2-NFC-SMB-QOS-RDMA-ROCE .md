---
description: Windows OS Host controller driver for Cloud, Storage and High-Performance computing applications utilizing NVIDIA’s field-proven RDMA and Transport Offloads
title: WinOF2-NFC-SMB-QOS
---

# WinOF-2 / WinOF Nvidia/Mellanox-  Setup / Drivers / Open Fabrics

NVIDIA Windows distribution includes software for database clustering, cloud, high performance computing, communications, and storage applications for servers and clients running different versions of Windows OS. This collection consists of drivers, protocols, and management in simple ready-to-install MSIs.

https://network.nvidia.com/products/adapter-software/ethernet/windows/winof-2/

WinOF and WinOF-2 distribution provides the following benefits:

1. Support Windows Azure Pack
2. Support traditional IP and Sockets based applications leveraging the benefits of RDMA
3. Support high-performance block storage applications utilizing RDMA
4. Cloud and virtualization:
5. NVGRE and VxLAN Hardware offload (ConnectX-3 Pro and ConnectX-4)
6. SR-IOV
7. Function per-port (ConnectX-4)
8. NDK with SMB-Direct
9. NDv1 and v2 API support in user space
10. Support Teaming and High-Availability
11. Support a variety of Windows Server and Client OS

![image](https://github.com/user-attachments/assets/33fa6487-1fc3-43d4-91d6-1c9327fafd18)




## Post Install Setup & Configuration Tests 

Screenshot from Hyper V Manager 

![image](https://github.com/user-attachments/assets/3b20c6f0-29b2-41a9-b732-f8a3f0b9717e)



```markdown

PS C:\Users\Administrator> Remove-NetQosTrafficClass
PS C:\Users\Administrator> Remove-NetQosPolicy -Confirm:$False
PS C:\Users\Administrator> New-NetQosPolicy "DEFAULT" -store Activestore -Default -PriorityValue8021Action 3
PS C:\Users\Administrator> Test-LogicalNetworkConnection  -Verbose "192.168.1.199"

ErrorMsg  TraceOutput                          RoundTripTime     Status  
--------  -----------                         ----------------  ---------
{      , Pinging 192.168.1.199 with 32 bytes of data:,
         Reply from 192.168.1.199: bytes=32 time<1ms TTL=128,
         Reply from 192.168.1.199: bytes=32 time<1ms TTL=128…}   Success

  Verifying Physical Nic:Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter

         Physical Nic  Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter can support SDN traffic.
         Encapoverhead value set on the nic is  160

  Verifying Physical Nic:Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter #2

         Physical Nic  Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter #2 can support SDN traffic.
         Encapoverhead value set on the nic is  160

PS C:\Users\Administrator> netsh int tcp set global rss = enabled

         Ok.

PS C:\Users\Administrator>  Mlx5Cmd.exe -QosConfig -SetupRoceQosConfig -Name "Ethernet" -Configure 2

  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0109
  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0109 finished
  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0009
  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0009 finished

        Lossless fabric with Dscp Value 26 with Adapter Specific Flow Control configuration configured successfully.

PS C:\Users\Administrator>  Mlx5Cmd.exe -QosConfig -SetupRoceQosConfig -Name "Ethernet 2" -Configure 2

  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0109
  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0109 finished
  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0009
  Restarting adapter PCI\VEN_15B3&DEV_1015&SUBSYS_009715B3&REV_00\4&12f54805&0&0009 finished

        Lossless fabric with Dscp Value 26 with Adapter Specific Flow Control configuration configured successfully.

```

![image](https://github.com/user-attachments/assets/c2e548d4-41e0-4eb0-a677-d12b5303e4b5)


## Configuration

### Set QOS, SMB, SMB-Direct, tcp  Policies 

```markdown
	
PS C:\Users\Administrator> New-NetQosPolicy "TCP" -store Activestore -IPProtocolMatchCondition TCP -PriorityValue8021Action 1
	
	Name           :tcp
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	IPProtocol     :TCP
	PriorityValue  :1
	
PS C:\Users\Administrator> New-NetQosPolicy "UDP" -store Activestore -IPProtocolMatchCondition UDP -PriorityValue8021Action  1
	
	Name:udp
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject  `   :
	IPProtocol     :DP
	PriorityValue  :1

PS C:\Users\Administrator> New-NetQosPolicy SMB -SMB -PriorityValue8021Action 3
	
	Name           :SMB
	Owner          :Group Policy (Machine)
	NetworkProfile :All
	Precedence     :127
	Template       :SMB
	JobObject      :
	PriorityValue  :3
	
PS C:\Users\Administrator> New-NetQosPolicy "SMBDirect" -store Activestore -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3
	
	Name           :smbdirect
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	NetDirectPort  :445
	PriorityValue  :3
	
PS C:\Users\Administrator> Enable-NetAdapterQos -InterfaceAlias "Ethernet"
PS C:\Users\Administrator> Enable-NetQosFlowControl -Priority 3
PS C:\Users\Administrator> gpedit.msc
PS C:\Users\Administrator>  get-netqospolicy -policystore activestore
	
	
	Name           :smb
	Owner          :Group Policy (Machine)
	NetworkProfile :All
	Precedence     :127
	Template       :SMB
	JobObject      :
	PriorityValue  :3
	
	Name           :tcp
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	IPProtocol     :TCP
	PriorityValue  :1
	
	Name           :udp
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	IPProtocol     :UDP
	PriorityValue  :1
	
	Name           :smbdirect
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	NetDirectPort  :445
	PriorityValue  :3
	
	Name           :default
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	Template       :Default
	JobObject      :
	PriorityValue  :3
	
PS C:\Users\Administrator> import-module NetQos
PS C:\Users\Administrator>  import-module DcbQos
PS C:\Users\Administrator> Set-NetAdapterQos -Name "Ethernet" -Enabled 1
PS C:\Users\Administrator> Enable-NetQosFlowControl 3,5
PS C:\Users\Administrator> New-NetQosPolicy "DEFAULT" -Default -PriorityValue8021Action 3 -DSCPAction 9
	
	Name           :DEFAULT
	Owner          :Group Policy (Machine)
	NetworkProfile :All
	Precedence     :127
	Template       :Default
	JobObject      :
	PriorityValue  :3
	DSCPValue      :9

PS C:\Users\Administrator> New-NetQosPolicy "TCP" -IPProtocolMatchCondition TCP -PriorityValue8021Action 3 -DSCPAction 16
	
	Name           :TCP
	Owner          :Group Policy (Machine)
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	IPProtocol     :TCP
	PriorityValue  :3
	DSCPValue      :16
	
PS C:\Users\Administrator> New-NetQosPolicy "UDP" -IPProtocolMatchCondition UDP -PriorityValue8021Action 3 -DSCPAction 3
	
	Name           :UDP
	Owner          :Group Policy (Machine)
	NetworkProfile :All
	Precedence     :127
	JobObject      :
	IPProtocol     :UDP
	PriorityValue  :3
	DSCPValue      :3
	
	Name :tcp1
	Owne           :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	JobObject  
	IPProtocol     :TCP
	IPDstPortStart :31000
	IPDstPortEnd   :31999
	PriorityValue  :0
	DSCPValue      :16
	
PS C:\Users\Administrator> New-NetQosPolicy "TCP2" -DSCPAction 24 -IPDstPortStartMatchCondition 21000 -IPDstPortEndMatchCondition 31999 -IPProtocol TCP -PriorityValue8021Action 0 -PolicyStore activestore
	
	Name           :tcp2
	Owner          :PowerShell / WMI
	NetworkProfile :All
	Precedence     :127
	IPProtocol     :TCP
	IPDstPortStart :21000
	IPDstPortEnd   :31999
	PriorityValue  :0
	DSCPValue      :24
	
PS C:\Users\Administrator> New-NetQosTrafficClass -name "TCP1" -priority 3 -bandwidthPercentage 16 -Algorithm ETS
	
	Name   Algorithm   Bandwidth(%)   Priority    PolicySet  IfIndex   IfAlias
	----   ---------  -------------- -----------  ---------  -------- ---------
	TCP1     ETS           16             3         Global
	
PS C:\Users\Administrator> New-NetQosTrafficClass -name "TCP2" -priority 5 -bandwidthPercentage 80 -Algorithm ETS
	
	Name    Algorithm  Bandwidth(%)  Priority    PolicySet IfIndex    IfAlias
	----   ---------  ------------- ---------- ----------- --------  ---------- 
	TCP2     ETS         80               5        Global
	
New-NetQosPolicy "ND10000" -NetDirectPortMatchCondition 10000 -PriorityValue8021Action 3
	
	Name           :ND10000
	
	Owner          :Group Policy (Machine)
	NetworkProfile :All
	Precedence     :127
	JobObject  :
	NetDirectPort  :10000
	PriorityValue  :3
	
PS C:\Users\Administrator> set-NetQosDcbxSetting -Willing 1
	
	Confirm
	Are you sure you want to perform this action?
	Set-NetQosDcbxSetting -Willing $true
	[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): y

```


### Get Setup info

```markdown

PS C:\Users\Administrator> Get-NetAdapterQos
  Name:Ethernet 2
  Enabled:True

Capabilities:    Hardware      Current
--------------  -----------   ----------
  MacSecBypass:NotSupported    NotSupported
  DcbxSupport:IEEE             IEEE
  NumTCs(Max/ETS/PFC):8/8/8    8/8/8

OperationalTrafficClasses:
  TC    TSA     Bandwidth    Prioriti
 -----  ------  -----------  ----------
  0    ETS        4%          0-2,4,6-
  1    ETS        16%               3
  2    ETS        80%               5
	
OperationalFlowControl:Priorities 3,5 Enabled
OperationalClassifications:
  Protocol    Port/Type    Priority
-----------  -----------  ----------
  Default                      3
  NetDirect     10000          3
  NetDirect      445           3
	
Name:Ethernet
Enabled:True
Capabilities:

  Hardware                     Current
-------------                 ----------
  MacSecBypass:NotSupported     NotSupported
  DcbxSupport:IEEE              IEEE
  NumTCs(Max/ETS/PFC):8/8/8     8/8/8
	
OperationalTrafficClasses:
   TC     TSA    Bandwidth    Priorities
-----  ----- ------------- ----------
   0     ETS     4%          0-2,4,6-7
   1     ETS    16%             3
   2     ETS    80%             5
	
OperationalFlowControl:Priorities 3,5 Enabled
OperationalClassifications:
  Protocol       Port/Type      Priority
 ----------    ------------   ----------
  Default                         3
  NetDirect     10000             3
  NetDirect      445              3
	

PS C:\Users\Administrator> Get-VMNetworkAdapter -VMName "Studio-Svr" | where -Property MacAddress -eq 00155D017802 | Set-VMNetworkAdapterVlan -Trunk -AllowedVlanIdList 10-1000 -NativeVlanId 1200

PS C:\Users\Administrator> Get-NetOffloadGlobalSetting | Select NetworkDirect
     NetworkDirect
   ---------------
       Enabled


PS C:\Users\Administrator> Get-SmbClientConfiguration | Select EnableMultichannel
  EnableMultichannel
 --------------------
        True

PS C:\Users\Administrator> ndinstall -i

Installing mlx5nd2 provider: already installed

Current providers:
       0000001001 - MSAFD Tcpip [TCP/IPv6]
       0000001002 - MSAFD Tcpip [UDP/IPv6]
       0000001003 - MSAFD Tcpip [RAW/IPv6]
       0000001004 - MSAFD Tcpip [TCP/IP]
       0000001005 - MSAFD Tcpip [UDP/IP]
       0000001006 - MSAFD Tcpip [RAW/IP]
       0000001007 - Hyper-V RAW
       0000001008 - RSVP TCPv6 Service Provider
       0000001009 - RSVP TCP Service Provider
       0000001010 - RSVP UDPv6 Service Provider
       0000001011 - RSVP UDP Service Provider
       0000001012 - AF_UNIX
       0000001013 - MSAFD L2CAP [Bluetooth]
       0000001014 - MSAFD RfComm [Bluetooth]
       0000001015 - MSAFD Pgm (RDM)
       0000001016 - MSAFD Pgm (Stream)
       0000001017 - NDv1 Provider for Mellanox WinOF-2
       0000001018 - NDv2 Provider for Mellanox WinOF-2

PS C:\Users\Administrator> Get-VM Studio-Svr | Set-VMNetworkAdapter -AllowTeaming On

```



### NFS & SMB  Configuration

```markdown 
PS C:\Users\Administrator> Get-NfsServerConfiguration

State                            :Running
LogActivity                      :{Mount, Read, Write, Create…}
CharacterTranslationFile         :Not Configured
DirectoryCacheSize (KB)          :128
HideFilesBeginningInDot          :Disabled
EnableNFSV2                      :True
EnableNFSV3                      :True
EnableNFSV4                      :True
EnableAuthenticationRenewal      :True
AuthenticationRenewalIntervalSec :999
NlmGracePeriodSec                :60
MountProtocol                    :{TCP, UDP}
NfsProtocol                      :{TCP, UDP}
NisProtocol                      :{TCP, UDP}
NlmProtocol                      :{TCP, UDP}
NsmProtocol                      :{TCP, UDP}
PortmapProtocol                  :{TCP, UDP}
MapServerProtocol                :{TCP, UDP}
PreserveInheritance              :False
NetgroupCacheTimeoutSec          :30
UnmappedUserAccount              :
WorldAccount                     :Everyone
AlwaysOpenByName                 :False
GracePeriodSec                   :240
LeasePeriodSec                   :120
OnlineTimeoutSec                 :180

PS C:\Users\Administrator> Get-NfsMappingStore

UNMServer               :P-HPC
UNMLookupEnabled        :True
ADDomain                :
ADLookupEnabled         :False
LdapServer              :
LdapNamingContext       :
LdapLookupEnabled       :False
PasswdFileLookupEnabled :False
PS C:\Users\Administrator> Get-NfsStatistics -Protocol "Mount"

Name              Protocol Version Value
----              -------- ------- -----
V1_MNT_NULL        MOUNT      1      0
V1_MNT_MOUNT       MOUNT      1      0
V1_MNT_DUMPMOUNT   MOUNT      1      0
V1_MNT_UNMOUNT     MOUNT      1      0
V1_MNT_UNMOUNTALL  MOUNT      1      0
V1_MNT_EXPORTLIST  MOUNT      1      0
V3_MNT_NULL        MOUNT      3      0
V3_MNT_MOUNT       MOUNT      3      0
V3_MNT_DUMPMOUNT   MOUNT      3      0
V3_MNT_UNMOUNT     MOUNT      3      0
V3_MNT_UNMOUNTALL  MOUNT      3      0
V3_MNT_EXPORTLIST  MOUNT      3      0

PS C:\Users\Administrator> Get-NfsClientConfiguration

State                :Running
CaseSensitiveLookup  :Disabled
DefaultAccessMode    :754
MountType            :SOFT
MountRetryAttempts   :1
RpcTimeoutSec        :8
ReadBufferSize (KB)  :1024
WriteBufferSize (KB) :1024
UseReservedPorts     :Enabled
Authentication       :{sys, Krb5, Krb5i, Krb5p}
TransportProtocol    :{TCP, UDP}

PS C:\Users\Administrator>  Get-NfsShare

Name       Availability             Path
----       ------------             ----
G          Standard (not clustered) G:\
Pyramid-CA Standard (not clustered) C:\cdp

PS C:\Users\Administrator> Get-SMBShare

Name               ScopeName Path                  Description
----               --------- ----                  -----------
ADMIN$             *         C:\Windows            Remote Admin
C$                 *         C:\                   Default share
cdp                *         C:\cdp
cdp$               *         C:\
G                  *         G:\
G$                 *         G:\                   Default share
IPC$               *                               Remote IPC
Users              *         C:\Users
WindowsImageBackup *         G:\WindowsImageBackup


PS C:\Users\Administrator> Get-SmbClientNetworkInterface

  Interface Index       RSS Capable     RDMA Capable     Speed         Addresses                                                                                      Friendly Name
----------------------  ------------  ---------------  --------     ----------------                                                                                 ----------------
15                        False             False       10 Gbps         {}                                                                                             Ethernet
7                         True             True         10 Gbps        {2603:8081:7600:146d:5151:b556:1c71:6075, fe80::687d:b2f1:eaf4:a6f1, 192.168.1.199}             vEthernet (Virtual-Switch)
44                        True             False        10 Gbps        {fe80::385d:c30e:f93c:3246, 192.168.10.2}                                                       vEthernet (v-Intertnal- Switch)
52                        True             False        10 Gbps        {fe80::ea97:4e28:9313:4e43, 172.31.208.1}                                                       vEthernet (WSL)
16                        False            True          0  bps        {fe80::9bd7:af8c:f252:136a}                                                                     Ethernet 2



PS C:\Users\Administrator> Get-SmbConnection

ServerName           ShareName                     UserName            Credential          Dialect      NumOpens
-----------------    -------------------     ---------------------   ----------------     ---------   -----------
studio-svr data      P-HPC\Administrator      P-HPC\Administrator           3.1.1                          3


PS C:\Users\Administrator> Get-SmbMultichannelConnection

Server Name Selected Client IP     Server IP     Client Interface Index Server Interface Index Client RSS Capable Client RDMA Capable
----------- -------- ---------     ---------     ---------------------- ---------------------- ------------------ -------------------
studio-svr  True     192.168.1.199 192.168.1.162 7                      2                      True               False
studio-svr  True     192.168.10.2  192.168.1.162 44                     2                      True               False


PS C:\Users\Administrator>  nfsadmin  mapping

The following are the settings on localhost

  Mapping Server Lookup       :Enabled
  Mapping Server              :P-HPC
  AD Lookup                   :Disabled
  AD Domain                   :

PS C:\Users\Administrator> nfsadmin server

The following are the settings on localhost

  Locking Daemon Grace Period :1 minutes 0 seconds
  Activity logging Settings   :Mount,Read,Write,Create,Delete,Locking
  Protocol for Portmap        :TCP+UDP
  Protocol for Mount          :TCP+UDP
  Protocol for NFS            :TCP+UDP
  Protocol for NLM            :TCP+UDP
  Protocol for NSM            :TCP+UDP
  Protocol for Mapping Server :TCP+UDP
  Protocol for NIS            :TCP+UDP
  Enable NFS V3 Support       :Enabled
  Renew Authentication        :Enabled
  Renew Authentication Interval :999 seconds
  Directory Cache             :128 KB
  Translation File Name       :
  Dot Files Hidden            :Disabled
  NetGroup Source             :none
  NIS Server                  :
  NIS Domain                  :
  LDAP Server or AD Domain    :
  LDAP naming context (DN)    :


PS C:\Users\Administrator>  Install-WindowsFeature -Name NFS-Client

  Success Restart Needed Exit Code  Feature Result
  ------- -------------- ---------  --------------
  True    No                       NoChangeNeeded {}

PS C:\Users\Administrator>  Enable-WindowsOptionalFeature -FeatureName  ClientForNFS-Infrastructure -Online -NoRestart

  Path          :
  Online        :True
  RestartNeeded :False

PS C:\Users\Administrator> nfsadmin server P-HPC listgroups
The following are the client groups

        P-HPC-NFS
    
PS C:\Users\Administrator> nfsadmin server P-HPC addmembers  P-HPC-NFS Studio-Svr

        The settings were successfully updated.

PS C:\Users\Administrator> nfsadmin server P-HPC addmembers  P-HPC-NFS P-HPC

        The settings were successfully updated.

PS C:\Users\Administrator> nfsadmin server P-HPC listmembers  P-HPC-NFS

The following are the members in the client group  P-HPC-NFS

        Studio-Svr
        P-HPC
```


## SRIOV CONFIGURATION

```markdown

Get-NetQosPolicy

Priority   Enabled    PolicySet        IfIndex IfAlias
--------   -------    ---------        ------- -------
0          False      Global
1          False      Global
2          False      Global
3          True       Global
4          False      Global
5          True       Global
6          False      Global
7          False      Global

PS C:\Users\Administrator> Get-NetQosTrafficClass

Name                      Algorithm Bandwidth(%) Priority                  PolicySet        IfIndex IfAlias
----                      --------- ------------ --------                  ---------        ------- -------
[Default]                 ETS       4            0-2,4,6-7                 Global
TCP1                      ETS       16           3                         Global
TCP2                      ETS       80           5                         Global
PS C:\Users\Administrator>  Get-NetQosDcbxSetting

Willing         PolicySet        IfIndex IfAlias
-------         ---------        ------- -------
True            Global

PS C:\Users\Administrator> Get-NetAdapterSriov

Name  :Ethernet 2
InterfaceDescription :Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter #2
Enabled  :True
SriovSupport :Supported
SwitchName  :Default Switch
NumVFs :32

Name  :Ethernet
InterfaceDescription :Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter
Enabled :True
SriovSupport  :Supported
SwitchName :
NumVFs :8


PS C:\Users\Administrator> Get-VMNetworkAdapter -VMName "Studio-Svr" | where -Property MacAddress -eq EAFFAB1C4B23

Name                   IsManagementOs       VMName        SwitchName        MacAddress        Status     IPAddresses
---------         ---------------------  ----------      ------------      -------------   ----------- ---------------
Network Adapter          False           Studio-Svr    Mellanox-IOV-Sw     EAFFAB1C4B23       {Ok}           {}
Network Adapter          False           Studio-Svr   Mellanox-Lx 4 En      00155D017802      {Ok}           {}
Network Adapter          False           Studio-Svr      Mlnx-LX4-EN        00155D017806      {Ok}           {}

PS C:\Users\Administrator> Get-NetAdapterRDMA

  Name                                 InterfaceDescription                Enabled     Operational    PFC        ETS
----------                    -----------------------------------------  ----------  -------------  -------     ------  
vEthernet (Mellanox-IOV-Sw)    Hyper-V Virtual Ethernet Adapter             True          True         NA         NA
vEthernet (Mellanox-Lx 4 En)   Hyper-V Virtual Ethernet Adapter #3          False         True         NA         NA
vEthernet (Mlnx-LX4-EN         Hyper-V Virtual Ethernet  Adapter #2         False         False        NA         NA
Ethernet 2                     Mellanox ConnectX-4 Lx 10/25GbE 2-por…       True          True         True      True
Ethernet                       Mellanox ConnectX-4 Lx 10/25GbE 2-por...     True          True         True      True


PS C:\Users\Administrator> Get-NetAdapterHardwareInfo

Name      Segment      Bus     Device    Function    Slot     NumaNode     PcieLinkSpeed     PcieLinkWidth      Version
----      --------   -------- ---------- ----------  --------  ---------  -----------------  -----------------  -------------
Ethernet2    0        1         0          1         5         0            8.0 GT/s           8                1.1
Ethernet     0        1         0          0         5         0            8.0 GT/s           8                1.1


PS C:\Users\Administrator> netstat.exe -xan | ? {$_ -match "445"}
  Kernel       7 Listener       192.168.1.199:445      NA                     0
  Kernel       7 Listener       [2603:8081:7600:146d:5151:b556:1c71:6075%7]:445  NA                     0
  Kernel       7 Listener       [fe80::687d:b2f1:eaf4:a6f1%7]:445  NA


PS C:\Users\Administrator> Get-NetAdapterSriov

Name  :Ethernet 2
InterfaceDescription :Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter #2
Enabled  :True
SriovSupport :Supported
SwitchName  :efault Switch
NumVFs : 2

Name  :Ethernet
InterfaceDescription :Mellanox ConnectX-4 Lx 10/25GbE 2-port OCP Adapter
Enabled :True
SriovSupport  :Supported
SwitchName :
NumVFs:8

PS C:\Users\Administrator> Get-VMProcessor -VMName Studio-Svr

  VMName        Count     CompatibilityForMigrationEnabled     CompatibilityForOlderOperatingSystemsEnabled
-----------   ---------  ---------------------------------    ------------------------------------------------
Studio-Svr       36                    False                                        False


PS C:\Users\Administrator> Get-ComputeProcess

Id  :B8A7189C-7910-4521-B5B6-A5361620CAE1
Type :VirtualMachine
Isolation :VirtualMachine
IsTemplate :False
RuntimeId  :b8a7189c-7910-4521-b5b6-a5361620cae1
RuntimeTemplateId :
RuntimeImagePath  :
Owner  :VMMS


PS C:\Users\Administrator> mlxconfig -d mt4117_pciconf0 s SRIOV_EN=1 NUM_OF_VFS=16

Device #1:
----------
Device type:ConnectX4LX
Name:SN37A28322_SN37A28323_Ax
Description:ThinkSystem Mellanox ConnectX-4 Lx 10/25GbE SFP28 2-port OCP Ethernet Adapter
Device:mt4117_pciconf0

    Configurations:               Next Boot             New
        SRIOV_EN                     True(1)              True(1)
        NUM_OF_VFS                    8                       16

 Apply new Configuration? (y/n) [n] : y
Applying... Done!
-I- Please reboot machine to load new configurations.

```




## Mellonoxnx Device Configuration

```markdown

PS C:\Users\Administrator> mlxconfig -d mt4117_pciconf0 q

Device #1:
----------

Device type:ConnectX4LX
Name:SN37A28322_SN37A28323_Ax
Description:ThinkSystem Mellanox ConnectX-4 Lx 10/25GbE SFP28 2-port OCP Ethernet Adapter
Device:mt4117_pciconf0

Configurations:                                     Next Boot
        MEMIC_BAR_SIZE                              0
        MEMIC_SIZE_LIMIT                            _256KB(1)
        FLEX_PARSER_PROFILE_ENABLE                  0
        FLEX_IPV4_OVER_VXLAN_PORT                   0
        ROCE_NEXT_PROTOCOL                          254
        PF_NUM_OF_VF_VALID                          False(0)
        NON_PREFETCHABLE_PF_BAR                     False(0)
        VF_VPD_ENABLE                               False(0)
        STRICT_VF_MSIX_NUM                          False(0)
        VF_NODNIC_ENABLE                            False(0)
        NUM_PF_MSIX_VALID                           True(1)
        NUM_OF_VFS                                  16
        NUM_OF_PF                                   2
        SRIOV_EN                                    True(1)
        PF_LOG_BAR_SIZE                             5
        VF_LOG_BAR_SIZE                             0
        NUM_PF_MSIX                                 63
        NUM_VF_MSIX                                 11
        INT_LOG_MAX_PAYLOAD_SIZE                    AUTOMATIC(0)
        PCIE_CREDIT_TOKEN_TIMEOUT                   0
        NETWORK_PORTS_NUMBER                        0
        ACCURATE_TX_SCHEDULER                       False(0)
        PARTIAL_RESET_EN                            False(0)
        SW_RECOVERY_ON_ERRORS                       False(0)
        RESET_WITH_HOST_ON_ERRORS                   False(0)
        PCI_BUS0_RESTRICT_SPEED                     PCI_GEN_1(0)
        PCI_BUS0_RESTRICT_ASPM                      False(0)
        PCI_BUS0_RESTRICT_WIDTH                     PCI_X1(0)
        PCI_BUS0_RESTRICT                           False(0)
        PCI_DOWNSTREAM_PORT_OWNER                   Array[0..15]
        CQE_COMPRESSION                             BALANCED(0)
        IP_OVER_VXLAN_EN                            False(0)
        MKEY_BY_NAME                                False(0)
        UCTX_EN                                     True(1)
        PCI_ATOMIC_MODE                             PCI_ATOMIC_DISABLED_EXT_ATOMIC_ENABLED(0)
        TUNNEL_ECN_COPY_DISABLE                     False(0)
        LRO_LOG_TIMEOUT0                            6
        LRO_LOG_TIMEOUT1                            7
        LRO_LOG_TIMEOUT2                            8
        LRO_LOG_TIMEOUT3                            13
        ICM_CACHE_MODE                              DEVICE_DEFAULT(0)
        TX_SCHEDULER_BURST                          0
        LOG_MAX_QUEUE                               17
        LOG_DCR_HASH_TABLE_SIZE                     14
        MAX_PACKET_LIFETIME                         0
        DCR_LIFO_SIZE                               16384
        NUM_OF_PLANES_P1                            0
        NUM_OF_PLANES_P2                            0
        IB_PROTO_WIDTH_EN_MASK_P1                   0
        IB_PROTO_WIDTH_EN_MASK_P2                   0
        ROCE_CC_PRIO_MASK_P1                        255
        ROCE_CC_CNP_MODERATION_P1                   DEVICE_DEFAULT(0)
        ROCE_CC_PRIO_MASK_P2                        255
        ROCE_CC_CNP_MODERATION_P2                   DEVICE_DEFAULT(0)
        CLAMP_TGT_RATE_AFTER_TIME_INC_P1            True(1)
        CLAMP_TGT_RATE_P1                           False(0)
        RPG_TIME_RESET_P1                           300
        RPG_BYTE_RESET_P1                           32767
        RPG_THRESHOLD_P1                            1
        RPG_MAX_RATE_P1                             0
        RPG_AI_RATE_P1                              5
        RPG_HAI_RATE_P1                             50
        RPG_GD_P1                                   11
        RPG_MIN_DEC_FAC_P1                          50
        RPG_MIN_RATE_P1                             1
        RATE_TO_SET_ON_FIRST_CNP_P1                 0
        DCE_TCP_G_P1                                1019
        DCE_TCP_RTT_P1                              1
        RATE_REDUCE_MONITOR_PERIOD_P1               4
        INITIAL_ALPHA_VALUE_P1                      1023
        MIN_TIME_BETWEEN_CNPS_P1                    4
        CNP_802P_PRIO_P1                            6
        CNP_DSCP_P1                                 48
        CLAMP_TGT_RATE_AFTER_TIME_INC_P2            True(1)
        CLAMP_TGT_RATE_P2                           False(0)
        RPG_TIME_RESET_P2                           300
        RPG_BYTE_RESET_P2                           32767
        RPG_THRESHOLD_P2                            1
        RPG_MAX_RATE_P2                             0
        RPG_AI_RATE_P2                              5
        RPG_HAI_RATE_P2                             50
        RPG_GD_P2                                   11
        RPG_MIN_DEC_FAC_P2                          50
        RPG_MIN_RATE_P2                             1
        RATE_TO_SET_ON_FIRST_CNP_P2                 0
        DCE_TCP_G_P2                                1019
        DCE_TCP_RTT_P2                              1
        RATE_REDUCE_MONITOR_PERIOD_P2               4
        INITIAL_ALPHA_VALUE_P2                      1023
        MIN_TIME_BETWEEN_CNPS_P2                    4
        CNP_802P_PRIO_P2                            6
        CNP_DSCP_P2                                 48
        LLDP_NB_DCBX_P1                             True(1)
        LLDP_NB_RX_MODE_P1                          ALL(2)
        LLDP_NB_TX_MODE_P1                          ALL(2)
        LLDP_NB_DCBX_P2                             True(1)
        LLDP_NB_RX_MODE_P2                          ALL(2)
        LLDP_NB_TX_MODE_P2                          ALL(2)
        ROCE_RTT_RESP_DSCP_P1                       0
        ROCE_RTT_RESP_DSCP_MODE_P1                  DEVICE_DEFAULT(0)
        ROCE_RTT_RESP_DSCP_P2                       0
        ROCE_RTT_RESP_DSCP_MODE_P2                  DEVICE_DEFAULT(0)
        DCBX_IEEE_P1                                True(1)
        DCBX_CEE_P1                                 True(1)
        DCBX_WILLING_P1                             True(1)
        DCBX_IEEE_P2                                True(1)
        DCBX_CEE_P2                                 True(1)
        DCBX_WILLING_P2                             True(1)
        KEEP_ETH_LINK_UP_P1                         True(1)
        KEEP_IB_LINK_UP_P1                          False(0)
        KEEP_LINK_UP_ON_BOOT_P1                     False(0)
        KEEP_LINK_UP_ON_STANDBY_P1                  False(0)
        DO_NOT_CLEAR_PORT_STATS_P1                  False(0)
        AUTO_POWER_SAVE_LINK_DOWN_P1                False(0)
        KEEP_ETH_LINK_UP_P2                         True(1)
        KEEP_IB_LINK_UP_P2                          False(0)
        KEEP_LINK_UP_ON_BOOT_P2                     False(0)
        KEEP_LINK_UP_ON_STANDBY_P2                  False(0)
        DO_NOT_CLEAR_PORT_STATS_P2                  False(0)
        AUTO_POWER_SAVE_LINK_DOWN_P2                False(0)
        NUM_OF_VL_P1                                _4_VLs(3)
        NUM_OF_TC_P1                                _8_TCs(0)
        NUM_OF_PFC_P1                               8
        VL15_BUFFER_SIZE_P1                         0
        NUM_OF_VL_P2                                _4_VLs(3)
        NUM_OF_TC_P2                                _8_TCs(0)
        NUM_OF_PFC_P2                               8
        VL15_BUFFER_SIZE_P2                         0
        DUP_MAC_ACTION_P1                           LAST_CFG(0)
        SRIOV_IB_ROUTING_MODE_P1                    LID(1)
        IB_ROUTING_MODE_P1                          LID(1)
        DUP_MAC_ACTION_P2                           LAST_CFG(0)
        SRIOV_IB_ROUTING_MODE_P2                    LID(1)
        IB_ROUTING_MODE_P2                          LID(1)
        PHY_FEC_OVERRIDE_P1                         DEVICE_DEFAULT(0)
        PHY_FEC_OVERRIDE_P2                         DEVICE_DEFAULT(0)
        WOL_MAGIC_EN                                True(1)
        PF_SD_GROUP                                 0
        ROCE_CONTROL                                ROCE_ENABLE(2)
        PCI_WR_ORDERING                             per_mkey(0)
        MULTI_PORT_VHCA_EN                          False(0)
        PORT_OWNER                                  True(1)
        ALLOW_RD_COUNTERS                           True(1)
        RENEG_ON_CHANGE                             True(1)
        TRACER_ENABLE                               True(1)
        IP_VER                                      IPv4(0)
        BOOT_UNDI_NETWORK_WAIT                      0
        UEFI_HII_EN                                 True(1)
        BOOT_DBG_LOG                                False(0)
        UEFI_LOGS                                   DISABLED(0)
        BOOT_VLAN                                   1
        LEGACY_BOOT_PROTOCOL                        PXE(1)
        BOOT_INTERRUPT_DIS                          False(0)
        BOOT_LACP_DIS                               True(1)
        BOOT_VLAN_EN                                False(0)
        BOOT_PKEY                                   0
        DYNAMIC_VF_MSIX_TABLE                       False(0)
        EXP_ROM_UEFI_x86_ENABLE                     True(1)
        EXP_ROM_PXE_ENABLE                          True(1)
        ADVANCED_PCI_SETTINGS                       False(0)
        SAFE_MODE_THRESHOLD                         10
        SAFE_MODE_ENABLE                            True(1)

```





### Hyper-V VMSwitchExtensionPortFeature


``` markdown

cmdlet Get-VMSwitchExtensionPortFeature at command pipeline position 1
Supply values for the following parameters:
VMName[0]: *
VMName[1]:

Id            :776e0ba7-94a1-41c8-8f28-951f524251b5
ExtensionId   :1EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortSecuritySettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :7a498fc4-8572-4fdc-92ab-7a6fc7042d53
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortRdmaSettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :c885bfd1-abb7-418f-8163-9f379c9f7166
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortOffloadSettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :776e0ba7-94a1-41c8-8f28-951f524251b5
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortSecuritySettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :952c5004-4465-451c-8cb8-fa9ab382b773
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortVlanSettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :c885bfd1-abb7-418f-8163-9f379c9f7166
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortOffloadSettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :776e0ba7-94a1-41c8-8f28-951f524251b5
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortSecuritySettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False

Id            :952c5004-4465-451c-8cb8-fa9ab382b773
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortVlanSettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :alse

Id            :c885bfd1-abb7-418f-8163-9f379c9f7166
ExtensionId   :11EC6134-128A-4A23-B12F-164184B48348
ExtensionName :Microsoft Virtual Ethernet Switch Native Extension
Name          :Ethernet Switch Feature Settings
SettingData   :Msvm_EthernetSwitchPortOffloadSettingData: Ethernet Switch Feature Settings (InstanceID = "Microsoft:B8A7189C-7910-4521-B5B6-A5361...)
CimSession    :CimSession: .
ComputerName  :P-HPC
IsDeleted     :False



### Validate Remote Config
```markdown
PS C:\Users\Administrator> New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\" -Name 'CredentialsDelegation'
New-Item: A key in this path already exists.
PS C:\Users\Administrator> New-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\CredentialsDelegation\" -Name 'AllowFreshCredentialsWhenNTLMOnly' -PropertyType DWord -Value "00000001"
New-ItemProperty: The property already exists.
PS C:\Users\Administrator> New-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\CredentialsDelegation\" -Name 'ConcatenateDefaults_AllowFreshNTLMOnly' -PropertyType DWord -Value "00000001"

ConcatenateDefaults_AllowFreshNTLMOnly :1
PSPath                                 :Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\CredentialsDelegation\
PSParentPath                           :Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows
PSChildName                            :CredentialsDelegation
PSDrive                                :HKLM
PSProvider                             :Microsoft.PowerShell.Core\Registry

PS C:\Users\Administrator> New-Item -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\CredentialsDelegation\" -Name 'AllowFreshCredentialsWhenNTLMOnly'
New-Item: A key in this path already exists.
PS C:\Users\Administrator> New-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\CredentialsDelegation\AllowFreshCredentialsWhenNTLMOnly\" -Name '1' -Value "wsman/Studio-Server"
New-ItemProperty: The property already exists.

```
