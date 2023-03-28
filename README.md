# Scan-the-Network-with-Zenmap
In this lab, I conducted scan and enumeration on the fictional organization's internal network using Nmap

The Namp is a command line-based utility that is available on all current operating systems and supports the discovery of hosts and services on a network. For the hackers, Nmap is one of the first utilities used to build a picture of the victim’s network.

Nmap is command line version

Zenmap is graphical interface version

In this lab, I will use Zenmap to scan the local area network. I will begin by running simple Ping on the Lan network to identify the hosts attached to the network.

# Ping to identify host on the LAN network

First open Nmap - Zenmap GUI icon

![1](https://user-images.githubusercontent.com/121040101/228093003-c0532125-c3c9-4a52-bbf4-00caaff4aa0f.PNG)

In the Zenmap, type “172.30.0.0/24”
In the target field to specify the 172.30.0.0/24 subnet as the scan target.
And in the profile menu, select Ping scan.

![2](https://user-images.githubusercontent.com/121040101/228093104-6c982773-351b-4b4f-b4e4-e9d87e47da65.PNG)

Press scan button

![3](https://user-images.githubusercontent.com/121040101/228093185-f81cb10c-300d-40c9-960a-1d5352bfc150.PNG)
It returned with 4 results representing the different machines that Nmap detected on the target network segmant.

Clicked “host“ pane, click “fileserver01”, then click the “Host Details” tab to see an organized summery of the information gathered during the scan

![4](https://user-images.githubusercontent.com/121040101/228093461-f1d90c81-e60a-4917-af6f-04a9d95a9631.PNG)

The Ping scan confirms that the machine is available and identified the host name, IP address, and MAC address.

BUT, it cannot identify ports, operating systems, or services.

# SYN scan to find open ports
In next step, I will conduct SYN scan. The SYN scan is form of TCP scan that is unintrusive to the target host, this is why it is also called “stealth scan”. In the SYN scan, it first creates a TCP packet with the SYN flag set and then sent to the specific port of the target (during TCP handshake, this would be first step in the three step). When target receives the SYN flag, there is 2 way of response from the target. 

1) If port is open, target sends back ACK flag
2) if port is closed, target clears the SYN flag and sent RST flag.

Since SYN scan is not meant to set up TCP connection, if Nmap receive the ACK flag, Nmap sends RST flag to let target forget about previous request.

This can be undetected since it does not establish a TCP connection, but SYN scan can be detected by firewall and Intrusion Detection Systems (IDS).  

In the command box, erase “–sn” and type “–sS” and press enter to overwrite the existing command and begin a SYN scan on the network.

![5](https://user-images.githubusercontent.com/121040101/228095291-f125333e-fa73-4dfe-be56-a847a0380699.PNG)

After completed the scan, click “fileserver01” and then click “Ports/Host” tab to display the ports and services detected by the SYN scan

![6](https://user-images.githubusercontent.com/121040101/228095329-a615fcfb-bcce-4c1d-bb12-400c61064e29.PNG)

In this SYN scan, I was able to identify the open ports and services running on the ports of the FileServer01, but not able to see the OS. I will do that next step.

# Operating System detection scan

In the next step, I will run another scan using a single Nmap switch. This time, I will use –o switch, which invokes an operating system detection scan.

This scan can guess the OS of each host. This is possible because each OS responds to specific network packets in unique ways. Nmap OS detection examine the responses and compare with the database with more than 2,600 known OS fingerprints and also find which version it is.

BUT this is not 100% accurate.

In the command box, erase “–sS” then type “–o” and press enter to begin an OS detection scan on the network

![7](https://user-images.githubusercontent.com/121040101/228095858-48a32ef3-128e-42b8-8c82-a5e06d8f6db6.PNG)

On the left pane, click the “pfSense-office”, then click host details tab to see an organized summary of the information about the host detected during the scan.

![8](https://user-images.githubusercontent.com/121040101/228096869-a4917a84-45f8-4fee-a84e-e4ab6b41281f.PNG)

The Nmap have determined that the OS is FreeBSD 11.2 with accuracy of 86%.

In the earlier SYN scan, Nmap identified the services running on the machines, but not the versions. In the next step, I will use the “–sV” switch to run service scan, which will attempt to identify the versions of the software running on open TCP ports.
 
 # Service scan
 
In the Service scan, Nmap sends packets to an open port and analyzes the response. The services’ responses will response with banner information that identifies the service and version. This scan can make more accurate guess of the OS types because of the additional information.

BUT this scan can take longer than previous scans.

In the command box, erase “–O” and type “–sV” and press enter to begin a Service scan on the network

![9](https://user-images.githubusercontent.com/121040101/228098160-8acfec3f-2a86-43f0-ac32-1b3fc5d19ff3.PNG)

One the left pane, click “fileserver01” and then “Port/Hosts” tab to display the ports and services detected by the Service scan.

![10](https://user-images.githubusercontent.com/121040101/228098216-f10a8aef-c756-4296-bee7-f470ef2c9bc0.PNG)

Next, I will click scan menu and select save all scans to directory.

