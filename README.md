# Routing in Computer Networks 


**# Routing Computer Network in depth**
**How a device communicate ?**

Each device has a unique  **Media Access Control Address **   using which the data or packets which are sent over a network are reached to correct device.

Basically when we try to send a data using  a **Hub Device** over the network  the message or frame sent from a computer is received by that hub device and that hub device transmits the frame to all system/computer connected to that hub and  informs the system or computer who may be the receivers connected to that hub. 

If this message is not destined to you or if the destination mac address not matches with the receiver mac address then drop the message and that device will not receive the frame (alternative for "message" terminology).

Now once we got the destined device the data which we got via like data is not sent directly over network we have to **serialize the data** before sending.

 so **data is serialized into bytes then into  signal and sent accordingly** 
 If connected to **ethernet** then via electric pulses we serialize and send 
 If connected to **wifi** then via radio frequency we serialize and send 
 If connected to **fibre** then via light we serialize and send 
 
So Data is serialized into bits and sent as signal this layer is called as **Physical layer in OSI model** 

Then it is sent up to Data link layer logical layer ultimately sending that to process or thread who ever requested 
 - Hub is like dum it don't know which system is connected to my
    port so it sends to all port
 - It has no intelligence

So to overcome that **Switches** came into picture

Switches on the other hand know the exact presence of each device connected to that as each device advertise their presence
so here we get the advantage. 
If A sends the data to B what the switch will do is It knows where the B is as each device advertise their presence so switch will not send message to all device connected to that It will get the message from A and then directly send the message to B via the port B is connected with out sending the message to C,D OR E any num of device .
This increases the performance way better than hub networking.

But What if there are multiple machines/system which are connected to different switches and let suppose if A want to send data to ZZZ where both devices are connected to different switches 
so as ZZZ is far away here, the switch which is connected to A will transmit the message across all devices   as it not found the device ZZZ  connected to that particular  switch  where device A is connected .
So the solution for this is Internet Protocol.
 MAC Address is one big  global network so it have to scan each network.
 Internet Protocol
 There are 2 Types:
 IPV4 and IPV6 
 IPV4 is a 32 bit IP (4 Bytes )  Address where the first 24 bit are the network part and the next 8 bit are the host part .
 The host part uniquely identifies each  device in a network .
 Hosts which are in the same network can use Link Address or Mac Address to communicate 
 192.168.1.3/24 -    192.168.1 This is the network part 24 bits or 3 bytes
 .3/24 - .3 is the host part which uniquely identifies the device in a network 
We can  check how many bits are allocated to network and host part using the following 2 methdos 

 1. /24 - Its a Classless Inter Domain Routing notation which specifies how many bits are allocated to network part and how may are allocated to host part
  
 3. 255.255.255.0 it can be represented as 11111111.11111111.11111111.00000000- A subnet mask is a 32-bit number that separates an IP address into two parts: the network ID and the host ID.
It tells devices which portion of the address belongs to the network and which  portion i.e host identifies individual devices\
255.255.255.0 - this is just an octal conversion of the 32 bit Ip
    2^8 is 256 but allocation starts from 0 so 0 to 255 
![image](https://github.com/user-attachments/assets/72b35e1a-4535-4b7f-b0b0-255e805a033f)
192.168.1.0 to 192.168.1.255
192.168.1.0 is network address → identifies the subnet
    192.168.1.255 is broadcast address → used to send data to all hosts in the subnet
    the usable host IPs are:
    192.168.1.1 to 192.168.1.254

    How to check if an IP is in my network?
    Consider the IPAddress youn want to check and its subnet mask
    ![image](https://github.com/user-attachments/assets/24b76198-b963-44a9-9daa-7ff4231c282c)
    This result (192.168.1.0) is the network address. If another IP (e.g., 192.168.1.4) gives the same result when ANDed with the subnet mask, then it's in the same network.
    If the result  gives something different network address  then the particular IP is not part of that subnet

If 2 devices are on the same  sub network then they should communicate using MAC Address but what if the devices are only having the IP Adress How can they communicate 
well there is another jargon here i.e ARP Address Resolution Protocol
What ARP will do is It takes the IP of the device B from Device A and will broad cast that IP to all device connected through switches.
What devices will do is It will read the IP and will see  if the received IP adsress is me or not.
If IP Address is of any device let suppose B then B will send its MAC Address to A so that they can establish the communication.

ARP only works on same subnet.
IPs of different network cannot communicate via ARP request
If you run a command ip neigh show 
you will get IP Address of the devices that communicated with this device along with their corresponding MAC Address
How do then talk to different network 
well meet another jargon called as GateWay Very Important 
It enables us to send packets to another device of different network
The Gateway is also called as next hop or the router and it belongs to all the subnetwork.
There could be multiple gateway in broader perspective
Devices are aware of their gateway (default gateway).
![image](https://github.com/user-attachments/assets/8baf721a-0289-4b02-a9b1-ade4b7318f80)

A Gateway device  includes multiple IPs registered  and if there is IP there is a MAC Address for each IPs  so Gateway also have MAC or link Addresses 
and  A single IP of the gateway is the default gateway of a subnetwork

Switches gets updated with the MAC of ecah device connected to that including the gateway which is also a device and have a MAC 









 




