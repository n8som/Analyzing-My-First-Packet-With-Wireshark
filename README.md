# Analyzing-My-First-Packet-With-Wireshark

<h2>Activity overview</h2>

As a security analyst, I’ll need to analyze network traffic to learn what type of traffic is being sent to and from systems on the networks I’ll be working with.

Previously, I learned about packet capture and analysis. Analyzing packets can help security teams interpret and understand network communications. Network protocol analyzers such as Wireshark, which has a graphical user interface or GUI, can help me examine packet data during my investigations. Since network packet data is complex, network protocol analyzers (packet sniffers) like Wireshark are designed to help me find patterns and filter the data to focus on the network traffic that is most relevant to my security investigations.

Now I’ll use Wireshark to inspect packet data and apply filters to sort through packet information efficiently.

<h2>Scenario</h2>

In this scenario, I’m a security analyst investigating traffic to a website.

I’ll analyze a network packet capture file that contains traffic data related to a user connecting to an internet site. The ability to filter network traffic using packet sniffers to gather relevant information is an essential skill as a security analyst.

I must filter the data to:

- identify the source and destination IP addresses involved in this web browsing session,

- examine the protocols that are used when the user makes the connection to the website, and

- analyze some of the data packets to identify the type of information sent and received by the systems that connect when the network data is captured.

Here’s how I’ll do this: First, I’ll open the packet capture file and explore the basic Wireshark graphic user interface. Second, I’ll open a detailed view of a single packet and explore how to examine the various protocol and data layers inside a network packet. Third, I’ll apply filters to select and inspect packets based on specific criteria. Fourth, I’ll filter and inspect UDP DNS traffic to examine protocol data. Finally, I’ll apply filters to TCP packet data to search for specific payload text data.

<h2>Task 1. Explore data with Wireshark</h2>

In this task, I must open a network packet capture file that contains data captured from a system that made web requests to a site. I need to open this data with Wireshark to get an overview of how the data is presented in the application.

1. Open the packet capture file by double-clicking the file called sample on the Windows desktop. Wireshark starts.

The packet capture file has the Wireshark packet capture file icon, which shows a shark's fin swimming above three rows of binary digits. The packet capture file has a .pcap file extension that is hidden by default by Windows Explorer and on the desktop view.

2. Double-click the Wireshark title bar next to the sample.pcap filename to maximize the Wireshark application window. 

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/c1f8b797-12d1-4e35-9b56-89ae524b9ea2)

A lot of network packet traffic is listed, which is why I’ll apply filters to find the information needed in an upcoming step.

For now, here is an overview of the key property columns listed for each packet:

- No. : The index number of the packet in this packet capture file
- Time: The timestamp of the packet
- Source: The source IP address
- Destination: The destination IP address
- Protocol: The protocol contained in the packet
- Length: The total length of the packet
- Info: Some information about the data in the packet (the payload) as interpreted by Wireshark

Not all the data packets are the same color. Coloring rules are used to provide high-level visual cues to help me quickly classify the different types of data. Since network packet capture files can contain large amounts of data, I can use coloring rules to quickly identify the data that is relevant to me. The example packet lists a group of light blue packets that all contain DNS traffic, followed by green packets that contain a mixture of TCP and HTTP protocol traffic.

3. Scroll down the packet list until a packet is listed where the info column starts with the words 'Echo (ping) request'.

Here we can see, ICMP, is the protocol of the first packet in the list where the info column starts with the words ‘Echo (ping) request’:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/961eacbc-3c01-4cbd-92e8-58c82d263aab)

<h2>Task 2. Apply a basic Wireshark filter and inspect a packet</h2>

In this task, I’ll open a packet in Wireshark for more detailed exploration and filter the data to inspect the network layers and protocols contained in the packet.

1. Enter the following filter for traffic associated with a specific IP address. Enter this into the Apply a display filter... text box immediately above the list of packets:

```ip.addr == 142.250.1.139```

2. Press ENTER or click the Apply display filter icon in the filter text box.

The list of packets displayed is now significantly reduced and contains only packets where either the source or the destination IP address matches the address I entered. Now only two packet colors are used: light pink for ICMP protocol packets and light green for TCP (and HTTP, which is a subset of TCP) packets.

3. Double-click the first packet that lists TCP as the protocol.

This opens a packet details pane window:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/487934e4-87f1-4f96-bfa4-da75b0027b56)

The upper section of this window contains subtrees where Wireshark will provide me with an analysis of the various parts of the network packet. The lower section of the window contains the raw packet data displayed in hexadecimal and ASCII text. There is also placeholder text for fields where the character data does not apply, as indicated by the dot (“.”).

Note: The details pane is located at the bottom portion of the main Wireshark window. It can also be accessed in a new window by double-clicking a packet.

4. Double-click the first subtree in the upper section. This starts with the word Frame.

This provides me with details about the overall network packet, or frame, including the frame length and the arrival time of the packet. At this level, I’m viewing information about the entire packet of data.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/25d1d636-abb0-445e-8ee3-47e8dec0d6b1)

5. Double-click Frame again to collapse the subtree and then double-click the Ethernet II subtree.

This item contains details about the packet at the Ethernet level, including the source and destination MAC addresses and the type of internal protocol that the Ethernet packet contains.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/245b49d9-f3c8-49c0-ac80-7e23b5837220)

6. Double-click Ethernet II again to collapse that subtree and then double-click the Internet Protocol Version 4 subtree.

This provides packet data about the Internet Protocol (IP) data contained in the Ethernet packet. It contains information such as the source and destination IP addresses and the Internal Protocol (for example, TCP or UDP), which is carried inside the IP packet.

Note: The Internet Protocol Version 4 subtree is Internet Protocol Version 4 (IPv4). The third subtree label reflects the protocol.

The source and destination IP addresses shown here match the source and destination IP addresses in the summary display for this packet in the main Wireshark window.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/e438b1ea-c2f7-43a4-9380-35f5ef715022)

7. Double-click Internet Protocol Version 4 again to collapse that subtree and then double-click the Transmission Control Protocol subtree.

This provides detailed information about the TCP packet, including the source and destination TCP ports, the TCP sequence numbers, and the TCP flags.

The source port and destination port listed here match the source and destination ports in the info column of the summary display for this packet in the list of all of the packets in the main Wireshark window.

Here we see port 80 is the TCP destination port of this TCP packet:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/165bfd02-5703-4f99-8c2d-dbc3254a637f)

8. In the Transmission Control Protocol subtree, scroll down and double-click Flags.

This provides a detailed view of the TCP flags set in this packet.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/81ca95dd-4f75-47c1-ad74-518fa376e5c7)

9. Click the X icon to close the detailed packet inspection window.

10. Click the X Clear display filter icon in the Wireshark filter bar to clear the IP address filter.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/1151864a-ea15-4872-b8c6-04a03f7a634e)

All the packets have returned to the display.

If I ever accidentally close the Wireshark application, I can reopen it by double-clicking the sample file on the desktop.

<h2>Task 3. Use filters to select packets</h2>

In this task, I’ll use filters to analyze specific network packets based on where the packets came from or where they were sent. I’ll explore how to select packets using either their physical Ethernet Media Access Control (MAC) address or their Internet Protocol (IP) address.

1. Enter the following filter to select traffic for a specific source IP address only. Enter this into the Apply a display filter... text box immediately above the list of packets:

```ip.src == 142.250.1.139```

2. Press ENTER or click the Apply display filter icon in the filter text box.

A filtered list is returned with fewer entries than before. It contains only packets that came from 142.250.1.139.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/2498226d-bbbb-47a9-95ac-b7e7737c9606)

3. Click the X Clear display filter icon in the Wireshark filter bar to clear the IP address filter.

4. Enter the following filter to select traffic for a specific destination IP address only:

```ip.dst == 142.250.1.139```

5. Press ENTER or click the Apply display filter icon in the filter text box.

A filtered list is returned that contains only packets that were sent to 142.250.1.139.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/3f3af57f-3eeb-4c15-b359-b89708669410)

6. Click the X Clear display filter icon in the Wireshark filter bar to clear the IP address filter.

7. Enter the following filter to select traffic to or from a specific Ethernet MAC address. This filters traffic related to one MAC address, regardless of the other protocols involved:

```eth.addr == 42:01:ac:15:e0:02```

8. Press ENTER or click the Apply display filter icon in the filter text box.

9. Double-click the first packet in the list. I may need to scroll back to display the first packet in the filtered list.

10. Double-click the Ethernet II subtree if it is not already open.

The MAC address I specified in the filter is listed as either the source or destination address in the expanded Ethernet II subtree.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/46e91e97-8234-47ec-b4a3-3f2b8a0df37d)

11. Double-click the Ethernet II subtree to close it.

12. Double-click the Internet Protocol Version 4 subtree to expand it and scroll down until the Time to Live and Protocol fields appear.

The Protocol field in the Internet Protocol Version 4 subtree indicates which IP internal protocol is contained in the packet.

Here we see, TCP, is the protocol contained in the IPv4 subtree from the first packet related to MAC address 42:01:ac:15:e0:02:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/50382142-b67e-46f7-ae46-2d89d2581a63)

13. Click the X icon to close the detailed packet inspection window.

14. Click the X Clear display filter icon in the Wireshark filter bar to clear the MAC address filter.

<h2>Task 4. Use filters to explore DNS packets</h2>

In this task, I’ll use filters to select and examine DNS traffic. Once I‘ve selected sample DNS traffic, I’ll drill down into the protocol to examine how the DNS packet data contains both queries (names of internet sites that are being looked up) and answers (IP addresses that are being sent back by a DNS server when a name is successfully resolved).

1. Enter the following filter to select UDP port 53 traffic. DNS traffic uses UDP port 53, so this will list traffic related to DNS queries and responses only. Enter this into the Apply a display filter... text box immediately above the list of packets:

```udp.port == 53```

2. Press ENTER or click the Apply display filter icon in the filter text box.

3. Double-click the first packet in the list to open the detailed packet window.

4. Scroll down and double-click the Domain Name System (query) subtree to expand it.

5. Scroll down and double-click Queries.

I’ll notice that the name of the website that was queried is opensource.google.com.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/4d55e072-de1f-41d7-98f5-4657fdd5799a)

6. Click the X icon to close the detailed packet inspection window.

7. Double-click the fourth packet in the list to open the detailed packet window.

8. Scroll down and double-click the Domain Name System (query) subtree to expand it.

9. Scroll down and double-click Answers, which is in the Domain Name System (query) subtree.

The Answers data includes the name that was queried (opensource.google.com) and the addresses that are associated with that name.

Here I see the IP address, 142.250.1.139, is displayed in the expanded Answers section for the DNS query for opensource.google.com:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/ee1d3d01-03a2-4f2c-af10-5f57f8a85a87)

10. Click the X icon to close the detailed packet inspection window.

11. Click the X Clear display filter icon in the Wireshark filter bar to clear the filter.

<h2>Task 5. Use filters to explore TCP packets</h2>

In this task, I’ll use additional filters to select and examine TCP packets. I’ll learn how to search for text that is present in payload data contained inside network packets. This will locate packets based on something such as a name or some other text that is of interest to me.

1. Enter the following filter to select TCP port 80 traffic. TCP port 80 is the default port that is associated with web traffic:

```tcp.port == 80```

2. Press ENTER or click the Apply display filter icon in the filter text box.

Quite a few packets were created when the user accessed the web page http://opensource.google.com.

3. Double-click the first packet in the list. The Destination IP address of this packet is 169.254.169.254.

Here we see the Time to Live value, 64, of the packet as specified in the IPv4 subtree:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/edf66a36-b5bb-4439-9dc0-feb09fae5d94)

Here we see, 54 bytes, is the Frame Length specified in the Frame subtree:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/40ef2dd4-6da7-4e2c-a22d-6212c811ed2c)

Here we see, 20 bytes, is the Header Length under the IPv4 subtree:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/cb6361f2-182a-4e03-8a95-d47145c92019)

Here we see, 169.254.169.254, is the Destination Address under the IPv4 subtree:

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/d2fb45ed-c1da-4c0a-9415-d1b4201167e6)

4. Click the X icon to close the detailed packet inspection window.

5. Click the X Clear display filter icon in the Wireshark filter bar to clear the filter.

6. Enter the following filter to select TCP packet data that contains specific text data.

```tcp contains "curl"```

7. Press ENTER or click the Apply display filter icon in the filter text box.

This filters packets containing web requests made with the ```curl``` command in this sample packet capture file.

![image](https://github.com/n8som/Analyzing-My-First-Packet-With-Wireshark/assets/110139109/6550e5c0-895b-4064-b0d9-dd68fdadd486)

<h2>Conclusion</h2>

I now have practical experience using Wireshark to

- open saved packet capture files,
- view high-level packet data, and
- use filters to inspect detailed packet data.

This is an important milestone on my journey toward understanding how to use network packet analysis tools to examine network traffic!

