1. Prepare ARP

<br>

To create a static mapping, we first need to disable dynamic ARP, and therefore automatic resolution on the interface:

`> interface > ethernet > edit [INTERFACE] > arp > [MODIFY value to disabled]`

(we disable this on the ether2 connection to client)

<br>

In the client machine we create a static ARP entry, featuring the router's IP and interface MAC address:

`C:\> arp -s 192.168.88.1  79-9a-18-39-86-c7`

And in the router we create an entry for the reverse:

`add [ENTRY]`

`edit [ENTRY] addr (replace with desired IP address)`

`edit [ENTRY] mac (replace with client MAC address)`
