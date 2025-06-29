# Computer-Networks


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
 192.168.1.3/24 -    192.168.1 This is the network part 24 bits 3 bytes
 .3/24 - .3 is the host part which uniquely identifies
 There is some correction here 
 /24 - It is the subnet which specifies how many bits are allocated to network part 




