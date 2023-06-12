# LLDP-Protocol

---Disabling and Enabling LLDP Globally---

Is the duration that a receiving device should maintain LLDP neighbor information before aging it. If this timerlldp holdtime 180
expires and no LLDP packet being received the neighbor information is wiped. Default is 120 seconds.
R6(config)#lldp holdtime 120

An interval at which the device sends LLDP updates to neighbor. Default is 30 seconds.
R6(config)#lldp timer 30

The delay time in seconds for LLDP to initialize on any interface. Default is 2 seconds
R6(config)#lldp reinit 3

-----Disabling and Enabling LLDP on an Interface--------
interface e0/0
!--No LLDP packets are sent on the interface --!
no lldp transmit

!--No LLDP packets are received on the interface--!
no lldp receive

!--LLDP packets are sent on the interface--!
lldp transmit

!--LLDP packets are received on the interface.--!
lldp transmit

!--LLDP packets are received on the interface.--!
lldp receive

!--Display LLDP counters, including the number of packets sent and received, 
number of packets discarded, and number of unrecognized TLVs  --!
show lldp traffic


-----Monitoring and Maintaining LLDP--------
#show lldp traffic
LLDP traffic statistics:
Total frames out: 100
Total entries aged: 0 (the number of expired records)
Total frames in: 30
Total frames received in error: 0 (total number of frames received with errors)
Total frames discarded: 0
Total TLVs discarded: 0 (number of TLVs removed during communication)
Total TLVs unrecognized: 0 (total number of TLVs received without recognition)

*TLV stands for "Type-Length-Value". This is a data structure used in network protocols to transmit information between network devices. The TLV structure includes the following fields:
Type: Specifies the type of information to be conveyed.
Length: Specifies the length of the value.
Value: contains the value of the information.


*Display information about neighbors, including device type, interface type and  number, holdtime settings, capabilities, and port ID. 
You can limit the display to neighbors of a specific interface or expand the display  to provide more detailed information*
R7#show lldp neighbors ethernet 0/0
Capability codes:
    (R) Router, (B) Bridge, (T) Telephone, (C) DOCSIS Cable Device
    (W) WLAN Access Point, (P) Repeater, (S) Station, (O) Other

Device ID           Local Intf     Hold-time  Capability      Port ID
R6                  Et0/0          120        R               Et0/0

Total entries displayed: 1

*Display information about interfaces where LLDP is enabled.
You can limit the display to the interface about which you want information*
R7#show lldp interface ethernet 0/0
Ethernet0/0:
    Tx: enabled
    Rx: enabled
    Tx state: IDLE
    Rx state: WAIT FOR FRAME



Vlan ID: - not advertised

*Display information about a specific neighbor. 
You can enter an asterisk (*) to display all neighbors, or you can enter the name 
of the neighbor about which you want information*
R7#show lldp entry *


Display global information, such as frequency of transmissions, the holdtime for 
packets being sent, and the delay time for LLDP to initialize on an interface
R7#show lldp
Global LLDP Information:
    Status: ACTIVE
    LLDP advertisements are sent every 30 seconds
    LLDP hold time advertised is 120 seconds
    LLDP interface reinitialisation delay is 2 seconds

Delete the LLDP table of information about neighbors
R7#clear lldp table\

Reset the traffic counters to zero.
R7#clear lldp counters
