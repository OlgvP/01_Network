# Building a simple network

**Addressing table :**

|   Devices  |      IP      |     Mask      |
|------------|--------------|---------------|
| PC-Robert  | 192.168.1.10 | 255.255.255.0 | 
| PC-Camille | 192.168.1.11 | 255.255.255.0 |
| PC-Renaud  | 192.168.1.12 | 255.255.255.0 |
| DNS server | 192.168.1.253| 255.255.255.0 |
| Web server | 192.140.1.10 | 255.255.255.0 |


**Resource Requirements :**

- 1 switch (Cisco 2960 with Cisco IOS version 15.0(2) image lanbasek9 or similar)
- 3 PCs (Windows 10)
- 1 Local router 
- 1 External router 

# Connecting all devices

 As a first step in this project I connected all devices with copper straight-through 
 cable and assigned an unique IP address to PC's, Dns server and Web server (IP adresses are in 
 addressing table). 
 At this point PC's can already connect with each other. We can check connection using "ping"
 on terminal on each PC.
 Then I added DNS server IP address for PC's and Web sever. *The DNS server translates domain*
 *names into IP addresses, making it easier for users to access websites and services without* 
 *needing to remember complex IP addresses.*
 I assigned IP address: 192.168.1.1 mask 255.255.255.0 for default gateway in all PC's and
 DNS server. *The default gateway is assigned to computers and DNS servers to provide them*
 *with a route for sending network traffic to destinations outside of their local network.* 
 *When a computer or DNS server needs to communicate with devices on different networks or* 
 *access resources on the internet, it sends data packets to the default gateway.* 
 *The default gateway acts as an intermediary, forwarding these packets to their intended destinations* 
 *through the appropriate network paths.* 
 
 I assigned the following IP addresses for:
(While assigning IP addresses to routers, I had to set the port status to 
  "on" for each output interface of both routers.)
- the output (Gig 6/0) of the Local router connected to the switch: 192.168.1.1, mask: 255.255.255.0
- the output (Gig 7/0) of the Local router connected to the switch: 192.168.2.1, mask: 255.255.255.0
- the output (Gig 7/0) of the External router connected to the Local router: 192.140.1.1 mask: 255.255.255.0
- the output (Gig 6/0) of the External router connected to the Web server: 192.168.2.2 mask: 255.255.255.0

# Configuration DNS server

To configure the DNS server, we need to click on our DNS server and then open the "Services" tab, 
select and enable the DNS service, and then enter the name and address of the website. In my project, 
I added the domain name "www.cisco.com" with the IP address 192.140.1.10. This is the address of my web server,
so when I enter the domain name in a web browser on any of the computers, 
it will display the webpage stored on the web server.

# Configuration Web server

In my simple network on my Web server I needed assign IP adress for: the output Fa0, DNS server and default gateway.
I did it in previous steps. 
*By clicking on Web server and opening HTTP in services we can add more web pages.*

# Configure static routing

*Static routing is needed to manually configure and define the routing paths in a network.*
*When a packet arrives at a router with static routing configured, the router consults* 
*its routing table to determine the appropriate next-hop router or interface for* 
*forwarding the packet towards its destination.* 
*It does not exchange routing information or participate in route discovery protocols.*

For configure static routing we need to go to configuration on the router and click
"static" in Routing tab. Then put network, mask and next hop for our static route.

In my Local router I added:
Network: 192.140.1.0
Mask: 255.255.255.0
Next hop: 192.168.2.2

In my External router I added:
Network: 192.168.1.0
Mask: 255.255.255.0
Next hop: 192.168.2.1

**Now my simple network should work properly. We can open web browser on the PC and** 
**put "www.cisco.com", then the webpage stored on our web server should be displayed**
 