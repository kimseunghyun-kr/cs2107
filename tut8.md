dest = 172.30.1.5
QID = 0x0003

ipconfig /all mac -> 04-7C-16-0C-2D-67
    wireshark ->     04-7C-16-0C-2D-67

it matches

DNS server
    60:29:d5:52:d8:2f

Source mac address belongs to the router.

(c)
Yes

(d)
Ok

(e)

GPT says

A canonical name, also known as a CNAME record, is a type of DNS record that maps one domain name to another. In the case of www.comp.nus.edu.sg, the canonical name is likely set to a different domain name that is not part of NUS (National University of Singapore).

This could be for a few reasons. One possibility is that the website is hosted on a server that is physically located outside of NUS, and the canonical name is set to the domain name associated with that server. Another possibility is that the website has been moved to a different domain name for branding or other reasons, but the original domain name (www.comp.nus.edu.sg) has been set up as a CNAME to redirect traffic to the new domain.

Regardless of the reason, setting up a CNAME allows a website to be accessed through multiple domain names, while still maintaining a single source for the website content.


2.
UDP packets correspond to the Zoom connection
real time connection is prioritized for zoom, while video quality can somewhat be compromised -> packet dropping is allowed instead

TCP packets corresponds to the HTTPS website as websites need to guarantee all their resources are being shown to the user who requested it

3. a)
VPN operates by encapsulating the original network packets with an additional layer of packets.

As VPN operates in the network layer, it works in between layer 2 and layer 3 (usually inseparable in practice)


b)
yes. the VPN can see where the destination IP of Alice's packets are

c) 
Most probably not. While the video data is encrypted,the attacker could use the data length to guess the video. However, data length - corresponding to video duration to guess which video alice is watching, is most likely insufficient as there are many videos with the same length on YouTube


d)
no. the mac address works at physical layer. VPN doesnt have access to the link layer protocol