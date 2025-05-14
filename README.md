# Analyze-Networks-Attacks

## Objective  
Identify the likely cause of a service interruption.

## Scenario
Receive an automated alert from a monitoring system indicating a problem with the web server. Attempts to visit the company’s website results in connection timeout error message in the browser.

A packet sniffer was utilized to capture data packets in transit to and from the web server. A large number of TCP SYN requests was noticed from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. 

The server was taken offline temporarily so that the machine can recover and return to a normal operating status. The company’s firewall was configured to block the IP address that was sending the abnormal number of SYN requests. IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. Manager was alerted about this problem quickly and the next steps was discussed to stop the attacker and prevent the problem from happening again.

## Identifying Type Of Attack
One potential explanation for the website’s connection timeout error message is a DoS attack. The logs show that the web server stops responding after it is overloaded with SYN packet requests. This event could be a type of DoS attack called SYN flooding.

## Explaination Of The Attack
When the website visitors try to establish a connection with the web server, a three-way handshake occurs using the TCP protocol. The handshake consists of three steps:
1. A SYN packet is sent from the source to the destination, requesting to connect.
2. The destination replies to the source with a SYN-ACK packet to accept the connection request. The destination will reserve resources for the source to connect.
3. A final ACK packet is sent from the source to the destination acknowledging the permission to connect.

In the case of a SYN flood attack, a malicious actor will send a large number of SYN packets all at once, which overwhelms the server’s available resources to reserve for the connection. When this happens, there are no server resources left for legitimate TCP connection requests.

The logs indicate that the web server has become overwhelmed and is unable to process the visitors’ SYN requests. The server is unable to open a new connection to new visitors who receive a connection timeout message.

