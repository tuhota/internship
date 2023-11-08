1. Prepare ARP

<br>

To create a static mapping, we first need to disable dynamic ARP, and therefore automatic resolution on the interface:

`> interface > ethernet > edit [INTERFACE] > arp > [MODIFY value to disabled]`

![interface](interface.png)

(we disable this on the ether2 connection to client)

<br>

In the client machine we create a static ARP entry, featuring the router's IP and interface MAC address:

`C:\> arp -s 192.168.88.1  79-9a-18-39-86-c7`

![client](cmdcommand.PNG)

And in the router we create an entry for the reverse:

`add [ENTRY]`

`edit [ENTRY] addr (replace with desired IP address)`

`edit [ENTRY] mac (replace with client MAC address)`

![addr](addr.png)

![arp print](arp.png)

Note the entry is not flagged with D (dynamic)

<br>

# 2. NAT setup

To setup the basic configuation for NAT we used 
	/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade.
	This changes the outgoing packets leaving the rounter on the ether1 interface.	
	To confirm that we have NAT available, we put /ip firewall nat print in the terminal to look for 
	the chain-srcnat and action=masquerade.
	By doing this we would be able to access the internet.	
	For a specific port and address we can go to IP -> Firewall -> NAT tab then you can add a NAT
	and you can decide what type of connection you want (tcp or udp), and also change the destination and 
	source IP and ports. 
	You can also change the chain to dstnat.

<img width="311" alt="details" src="https://github.com/tuhota/internship/assets/109631279/8a0ae422-8be6-4b65-9e8d-8a9e4a7eead6">


<img width="670" alt="NAT" src="https://github.com/tuhota/internship/assets/109631279/50e122f9-5e70-4474-8fee-f6b1ecd40a4d">




# 3. Load balancing

There are multiple methods that can be employed for load balancing we chose PCC (per-connection-classifier) as this can be configured on the one router. We don't have access to multiple WAN connections but the example shows how we would divide traffic based on src-address:



