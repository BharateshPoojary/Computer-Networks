## Key Point
 
- Frame -It includes IP packet ,source and destination MAC Address.
- IPpacket - It includes the source and destination IP along with the Actual Payload Data
 
## How a device communicate ?

Each device has a unique  **Media Access Control** Address using which the data or packets which are sent over a network are reached to correct device.


Basically when we try to send a data (frame) in a  **Hub Environment** over the network  the message or frame sent from a computer/machine is received by that hub device and that hub device transmits the frame to all computer/machines connected to that hub. 

## NOTE
Devices before sending frame have to do ARP(Address Resolution Protocol) **what is ARP we covered this in detail below**  
In Short we do ARP to know destination machines MAC ADDRESS currently the sender machine only knows  destination machine IP Address but for sending any type of data irrespective in the same subnetwork we need the destination machines MAC Address.

### What the hub will do is ?
Once we got the destination machines MAC Address.  
The sender machine will prepare a frame which includes source and destination IP and Mac Address along with payload inside the packet.  
Once Frame is ready it will send it to HUB .   
Hub will send the frame to all the ports connected from devices and will tell each device that  
If this message/Frame is not destined to you or if the destination MAC address not matches with the receiver MAC address then drop the message/Frame and that device will not receive the frame (alternative for "message" terminology).

Now once we got the destined device(MAC Address matched with a device) , it will unpack the packet and will receive the data sent to it  

## Remember
Data is not sent directly over network we have to **serialize the data** before sending.
## Data Serialization
 **Data/Frame is serialized into bytes then into  signal and sent accordingly** 
- If connected to **ethernet** then via electric pulses we serialize and send 
- If connected to **wifi** then via radio frequency we serialize and send 
- If connected to **fibre** then via light we serialize and send 
 
  
So Data is serialized into bytes then bits and sent as signal this layer is managed by  **Physical layer in OSI model** 

**Data Link Layer** which is the second layer in OSI Model ensures that the Packets or Frame are  sent correctly over network  

ultimately sending the payload  to process or thread who ever requested 
- Hub is like dum it don't know which system is connected to my
port so it sends the frame to all port
- It has no intelligence

## Switches
So to overcome that **Switches** came into picture

- Switches on the other hand know the exact presence of each device connected to it as each device advertise their presence  
- so here we get the advantage. 
- If A sends the data to B what the switch will do is It knows where the B is as each device advertise their presence so switch will not send message to all device connected to that.
-  It will get the message from A and then directly send the message to B via the port B is connected.
-  With out sending the message to C,D OR E any num of device .
- This increases the performance way better than hub networking.



### Internet Protocol 
- But What if there are multiple machines/system which are connected to different **switches** and let suppose if A want to send data to ZZZ where both devices are connected to different switches..  
- so as ZZZ is far away here, the switch which is connected to A will transmit the message across all devices   as it not found the device ZZZ  connected to that particular  switch  where device A is connected .
- So the solution for this is **Internet Protocol**.
 - **MAC Addresses is one big  global network** It is a unique address given to each device which are present globally  
- so as switches have to scan each network it becomes difficult to scan such a global network .
 
- There are 2 Types:
- IPV4 and IPV6 
- IPV4 is a 32 bit IP (4 Bytes )  Address 
- e.g In Ip 192.168.1.25/24 where the first 24 bit are the network part and the next 8 bit are the host part .
- The host part uniquely identifies each  device in a network .
- **Hosts which are in the same network can use Link Address or Mac Address to communicate** 

### We can check how many bits are allocated to network and host part using the following 2 methdos 

    1. /24 - Its a Classless Inter Domain Routing notation which specifies how many bits are allocated to network part and how may are allocated to host part 
    - In this case 24 bits for network part and rest for host part 

    2. 255.255.255.0 - It can be represented as 11111111.11111111.11111111.00000000 - A subnet mask is a 32-bit number that separates an IP address into two parts: 
    - The network ID and the host ID.
    - It tells devices which portion of the address belongs to the network and which  portion belongs to host.

### What is host ? 
-  Host identifies individual devices in a subnetwork or in a network

### The Mystery behind 255.255.255.0
    255.255.255.0 - this is just an octal conversion of the 32 bit Ip
    2^8 is 256 but allocation starts from 0 so 0 to 255 
    ![image](https://github.com/user-attachments/assets/72b35e1a-4535-4b7f-b0b0-255e805a033f)
    192.168.1.0 to 192.168.1.255 total 254 hosts can be connected in this subnet.
    192.168.1.0 is network address → identifies the subnet
    192.168.1.255 is broadcast address → used to send data to all hosts in the subne
    The usable host IPs are: 192.168.1.1 to 192.168.1.254

### How to check if an IP is in my network?
    Consider the IPAddress you want to check and its subnet mask
    ![image](https://github.com/user-attachments/assets/24b76198-b963-44a9-9daa-7ff4231c282c)
    This result (192.168.1.0) is the network address of your Ip so if any Ip gives you this network address then its in your network . 
    If another IP (e.g., 192.168.1.4) gives the same result when ANDed with the subnet mask, then it's in the same network.
    If the result  gives something different network address  then the particular IP is not part of that subnet


- If 2 devices are on the same sub network then they **should communicate using MAC Address** but Only IP Address is not enough for sending the data then,
### How should they communicate ?
well there is another jargon here i.e **ARP Address Resolution Protocol**
What ARP will do is 
- It takes the IP of the device 'B' from Device 'A' and will broad cast that IP to all device connected through switches.
What devices will do is 
- It will read the IP and will see  if the received IP address is me or not.
- If IP Address is of any device let suppose B then B will send its MAC Address to A so that they can establish the communication.

 
- Different devices of different network cannot communicate via ARP request Directly 
If you run a command 
```bash  ip neigh show```  
- you will get IP Address of the devices that communicated with this device along with their corresponding MAC Address

### How do then talk to different network? 
- well meet another jargon called as **GateWay** Very Important 
- It enables us to send packets to another device of different network
- The Gateway is also called as next hop or the router and it belongs to all the subnetwork.
- There could be multiple gateway in broader perspective
- Devices are aware of their gateway (default gateway).
![image](https://github.com/user-attachments/assets/8baf721a-0289-4b02-a9b1-ade4b7318f80)

- A Gateway device  includes multiple IPs registered  and if there is IP there is a MAC Address for each IPs .
- so Gateway also have MAC or link Addresses and  
- A single IP of the gateway is the default gateway of a subnetwork

- Switches gets updated with the MAC of each device connected to that including the gateway which is also a device and have a MAC.
- Switches know where in which port which device is connected 

- Let suppose device "A" wants to send data to device "B"
-  so what ARP will do It consider the IP of that destined device and will broadcast to all devices connected through the switch even if it is  a gateway.
- How the device A got the IP address of Device B it is by DNS or something (not talked in detail )
#### The ARP REQUEST is not sent through the other networks.

    Once it will get the device with the same IP Address the Device "B" will sent its Mac to "A"  and A will send or communicate with B this is the case when the devices  are in same subnet with gateway connected.

How the data is sent here?
- we  know the direct link address we send an IP Packet which includes source MAC A and destination MAC B and the source IP , destination IP along with the data so its like all this data is encapsulated in a single frame and sent to B .
- B will receive that and it will unpack the frame and it will get an IP Packet over there and it will see that this Ip is me only and what ever instruction it has in PACKET LIKE tcp udp it will just deliver it 
- In case of TCP I will send the IP Packet in front TCP segment . which includes destination port and source port and then you put your http protocol or ssh protocol or any other on top of TCP .
- Any thing on top of IP its just Data 
- Data is encapsulated in a data link frame 


## Internetwork Communication
But what if device "A" wants to send Data to C or D which both are in different subnetwork 
lets talk about Internetwork Communication 

- The only possible way to communicate is using the **gateway** (If you want to do ARP you have to be in the same network)

- If you not get the the destined Ip in your subnetwork then you send that IP to the **default gateway**
-  so for which you need gateway IP so you get it 
- now you will do ARP to broadcast the message to get the gateways MAC Address but there is a concept of **ARP Poisioning** here which enables hackers to tell that I am your destined Ip which is not and then we send the packet to the hacker device so this is how data is corrupted well that another topic.

- Coming back to broadcasting to each device in a subnet so gateway will read the broad cast and will unpack it and sees that it is his IP so It will give its mac to source device.
- now the source device  will send a frame which includes the MAC Address of both device to ensure source and destination device also the main thing is this **frame  includes the IP Packet which includes the source and destination IP , destination IP means the IP of device which is present in other network** so first the Frame will be received by router and it will see that the Frame is intended to me but the IP packet inside is not for me it is having something different destination IP 
- so as the router is a linux machine and OS Kernel has a feature something called **IP Forwarding** 
- Our machine can also be turned as router by enabling this Ip forwarding to true and it will also forward the IP To all the devices of the network
- so the frame is for gateway but the IP inside it is not for it so it will check its registered networks and sees if any network matches with the destination IP if any matches the router will send the packet through that ethernet cable.
- Now gateway/router can do ARP as it is also in the same network of destined device  to get the Mac Address 
-  ARP will broadcast the message and the destined device will read that message and will say its my IP and it will send its MAC to the gateway .
- Now Gateway will send the packet in a frame to the destined device .
- This frame includes source and destination MAC and the Ip packet inside it includes the source and destination Ip (note the source MAC IS routers MAC where as source IP is the  IP of the device of another network ) and this is how routing /  data is sent   across networks.

### Different Scenario
- (There are some cases where we have to change the source IP like say we are in our private network 
- let say **192.168.0.0/16** and we have to talk to **google.com** so at that time router will not send our private  IP to google and google not even know what 192.168.0.0/16 this IP  mean as it is private .

coming back, 
- There are bunch of Private network which you can check so here in this case source IP gets change and this process is known as **Network Address Translation (NAT)**

- Now the Frame is received by destined device it unpacks the frame and sees that Its his MAC and also the Ip belongs to it so now kernel will deliver the message to the application (we will get to how it sends from kernel to application in depth is OS ).

- Now that destined device will also broadcast a message with the  Ip of our source one which is  residing  on other network so router will read the message and it is having  similar network registered with it so  router will add the layer 2 frame i.e its MAC and sends it to the device which broadcasted .
- layer 1 is the IP packet.
- Now the device got a frame it cracks it and gets the MAC and establishes a communication with gateway 

- Now as the gateway receives the frame it unpack it sees that MAC  is intended to it but the IP inside it is not for it so it will do **IP Forwarding** here and now it will broadcast the message with the Destination Ip and this process continues this is how **INTERNETWORK ROUTING WORKS**.  

- In home technically,  you have one gate way which connects you to the internet but in Internet you will have **multiple gatways**. 
- There are ISP'S Internet Service Provider like Frontier,Verizon like they have different routers and each router have different subnets. 
- This subnets are reserved for particular ISPs so the thing is you cannot have one default gateway there could be multiple gateways 
- so in that case **how it knows from which router the frame should go.** 

## Routing Table
- So to overcome this problem meet the ROUTING TABLE (It WILL TELL IF YOU WANT TO GO HERE OR TO THIS IP THEN GO FROM THESE ROUTER )    
- It includes a bunch of field like 
  ```  
    1.Where do you want to go?(Destination  network)
    2.What is the nexthop (gateway)?
    3.Is it direct link or not?(If it is in a same subnet)
    4.Weight (metric) - which router should you prior so that you can go fastly
    5.Which interface should I go through is it a ethernet interface or a wifi 
    
Each OS has its own routing table   
MAC is having its own ,  
Windows is having its own,  
But the fields are the same 
the Table is already configured in our machine and we can manually configure that as well like   
If you want to go google then go from this machine you can send all the traffic to a single machine 
and from there you can send the traffic to where they are intended to go.
![image](https://github.com/user-attachments/assets/6863c07f-4c1a-48aa-ba6b-d39286247bc2)

- As per the above image line 3 if you are going to any network you should go from 192.168.1.1  and there is no direct link you cannot do ARP here the higher the weight the lower the priority given to the router as there could be router who have lower weight so we prefer going through that so that we can reach fastly
- If you are going to any network then go through this Network Interface i.e in line 3 there is ethernet 1 .**(we should go from there if we are going any where )**
- Next if you want to go in this network  10.0.0.0/24 then there is no nexthop, there is a direct link means you can do ARP and the lower the weight the higher the chances of getting faster over there and we should go through ethernet 2.

![image](https://github.com/user-attachments/assets/353f01fd-8456-4cdf-a49b-a074119d34af)
- As per the image if you want to go to 172.16.6.2 then go through 10.0.0.6 gateway 
- if you are going to any where then go throught this 10.0.0.1 gateway
 - This is the routing table which we can configure either in each machine of subnetwork or we can also configure this routing table in a router itself   
- But the thing is everytime the machine want to communicate with any device first it has to go through its default gateway which would be slower but
 -  If we need faster then we have to configure it in every machine so there is trade offs 

![image](https://github.com/user-attachments/assets/6ede3639-373e-4bfb-8121-e1907e6009cb)

### Who updates the routing table ?
``` 
Kernel,DHCP,Other protocols like OSPF,BGP or even manually  
DHCP-Dynamic Host Control Protocol which assigns the IP address for us if we dont want to statically configure by us .
OSPF-Open shortest protocol first
BGP-Border Gateway Protocol on top of which the internet runs on
All of this  do is just update the routing table
![image](https://github.com/user-attachments/assets/de09dabf-cadd-4071-8f6f-213b05a1b1f7)
```
### OHCP What it will do is ? 
First It will make a list that from this Machine through this particular  Network Card what are all the possible Interfaces what are the possible direct links based on that it determines the shortest path to send data and this Shortest Path it writes in the routing table
### Kernel 
Kernel is respondible for following the instructions of routing table 

### Autonomous network
There are certain autonomous network which are default configured in routing table like if you want to go google go through this network etc

![image](https://github.com/user-attachments/assets/57831141-16d7-4856-90cb-b6ce9e6bffc8)


the above is the routing table of  a windows OS  
- By default for any destination network the default gateway will be 192.168.43.50 and the interface 192.168.43.94  defines  a partcular IP for this device if connected though a wifi in my case as I am connected to that so NIC (Network Interface ) changes as per the device which you are connected .
- Next all routes we can directly reach through a link no gateway required where the 127.0.0.0 if this is the destination and if this  127.0.0.1 is the source IP then its called a **loopback address** (It means Redirecting or pointing to same machine ).  

![image](https://github.com/user-attachments/assets/1a4106a5-fc5a-4dc2-bd8b-15120d4fd35c)

![image](https://github.com/user-attachments/assets/ee179945-e245-404d-973c-3905ae6e8916)

#### The above is the route table in a linux machine
- For any destination network i.e 0.0.0.0/0 your default gateway will be 192.168.4.1 with the device as ethernet  and source IP or the Network Interface for this device is 192.168.7.179 IP for this device if connected to ethernet with metric 100 that means it gets the priority as compared to second one which is connected through a wifi (the traffic is sent faster from here then 2nd one) 
- The source IP is assigned by DHCP 

- If the request is from a docker virtual interface i.e from IP 127.17.0.1 then your network destination will be 127.17.0.0/16 so my linux machinme is configured with a docker machine where if I try to connect with my docker host like 127.17.0.2 then it send the request from this 127.17.0.1 IP as per the routing table see the video to get clearity 
- Rest  all are direct link we just have to do ARP ,  we can directly communicate through the MAC 

```
we can see ethernet has lower metric as compared to wifi so it is preffered but we can also manually configure like which one to choose when going to this particular destination.
```


![image](https://github.com/user-attachments/assets/535bd814-a0e1-4db5-a0cc-58258a612437)

https://bharat-miscellaneous-bucket.s3.ap-south-1.amazonaws.com/WhatsApp+Video+2025-07-03+at+11.17.30+PM.mp4

- we have example in the above video where a linux/ubuntu machine(192.168.7.179) is connected with a docker machine  with the docker0 interface 172.17.0.1 as shown in the routing table above.
- and as per the video we are trying to connect to a docker host/IP  172.17.0.2 which is having a single docker container   
- so as per the routing table we can  go to any host via our docker 0 interface . 
-  we connected to our  docker host via my machine which had docker host already configured in route table  and now I can connect with my postgres DB .
- But Later we can see he tried to connect from other machine which is a MAC device it tried but it failed why because the docker machine is connected from my that linux machine and not from my mac machine .
- So what he did is he added a command telling connect to 172.17.0.2 by going through this network interface 192.168.7.179 
- so both this mac and linux machine as they are connected to same ethernet which is having a default gateway 192.168.4.1 .
- So my mac machine will ARP **(REMEMBER BOTH MAC AND LINUX ARE CONNECTED TO SAME ETHERNET SO THEY ARE IN SAME SUBNET )**
-   AND my mac machine will broad cast the message telling I want to connect to 172.17.0.2 - my linux machine will read the message ok I am not having this IP but I have a network Interface from which you can go there 
- so my linux machine will give his IP to Mac machine now mAC Machine will wrap the IP packet in frame and will send to linux machine 
-  my linux machine will unpack the frame and sees the IP packet is not mine so it will forward that IP **(IP Forwarding enabled in linux machine so  we can say it act like a next hop/router/gateway for Mac machine )** to other network interface i.e 172.17.0.1  .
- so  192.168.7.179 - our linux machine IP Connected through ethernet  will forward the request to 172.17.0.1 Interface which is my docker Interface   and boom we connected to our docker network and then we connected to our postgresdb which is there on IP/docker host 172.17.0.2  having a single docker container .
- For getting  your machines routing table 
```
route print
```
# So this is how the entire Routing happens and packets are sent over a network will cover in more depth later
