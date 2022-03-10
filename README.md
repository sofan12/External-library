# High level summary CSE 310
Python API used: dpkt
For part A, 
I first open the inputted PCAP file by using reading bytes of the file, and turn the read bytes into ethernet. 
And use the function in dpkt, PCAP to read the file. Then the ethernet that contains data of ip of the packets, then get the data of the IPs to reach to the TCP by filtering the tcp packets.
Next, to estimate the amount of TCP flows, using if each TCP file has a SYN flag to determine the beginning of a flow, which each TCP flow starts with a SYN. Also, since each TCP flows has a FIN packet to indicate the end of a TCP flow.
Use the flag of the packets to determine the amount of the flows. As for the 2 transaction after the TCP connection is set up, find the first 2 packets sent and received (total of 4 packets) 
by filtering of packets’ destination port and source port after the first ACK packet, which is the confirmation of the set up of a TCP connection. 
For the source port, destination port, source IP address, and destination IP address, I use the ip internet to string in dpkt to get the source IP address and destination IP address of the packet of SYN, as well as source port and destination port of the SYN packets. 
As for the sender throughput, I get the bytes of every packet using Netflow in dpkt to get the bytes of sending and acknowledging between packets in each flow, , which is the sender throughput over a period. 
I exclude the bytes transmitted in the 3-way handshake process and the bytes transmitted in the FIN packet, to do so, I use the flags of tcp to filter these packets
Part B 
Congestion estimation: As when is a packet loss, there would possibly be a congestion occurs. So, when there is a large amount of consecutive rows of packets with the same ports, ip addresses, same sequence number, and same ack number. Then it would be the congestion control. 
Therefore I filter and sum up the byte size and window size correspondingly. 
For retransmission due to timeout and triple duplicate ack. 
I first locate the retransmission packets and then determine the packet retransmitted 
due to timeout or triple duplicate ack respectively according to the packets around these packets with the info of out of order or DUP. 
