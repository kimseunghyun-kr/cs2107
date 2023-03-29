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


1(a)

client Hello initiates with security suite etc
server hello returned with cert containing server public key
client verifies(authentificates) cert -> through shared trusted root cert auth

client

1(b)

--gpt--
On the server-side, the application can use a variety of techniques to verify the client's identity. For example, the server can require the client to present a valid certificate during the TLS handshake process, which can then be verified against a list of trusted certificate authorities. The server can also require the client to authenticate with a username and password or other credentials.

On the client-side, the application can use a combination of cookies, session tokens, and other mechanisms to track the user's identity and ensure that subsequent requests from the client are authenticated and authorized.


1(c)

--gpt--
the MITM sits in the Transport - Network Layer at least, as it needs to obtain the IP address of the victim, in order to constantly capture the packets sent by the victim.
(which can be done via DNS spoofing or rogue routers)

1(d)
the client and attacker obtain the server's public key through initiating the TLS handshake, by receiving the server's certificate signed by a shared CA

1(e)
The attacker does not know the second session key, as by the assumpn provided by DH key exchange that is used to generate the session key between the client and the server

1(f)
In the introduction of RFC5746, "initial traffic" refers to the data that is exchanged between the client and server during the initial TLS handshake before any renegotiation takes place.

from the server's perspective, k1 is used to protect the initial traffic

1(g)
1 is not, 2 is

1(h)
In the introduction of RFC5746, "client traffic" refers to the data that is sent from the client to the server during a TLS session.

thus 2 is used

1(i), the confidentiality of the report could have been compromised, if the attacker could inject a request to show Alice's report.

--zechen --
does not compromise -- ? -> probably due to message being encrypted and not being sent via plaintext -> read the slides


(j)
the attacker can modify the header of message m to m tilda
the attacker can steal information present within the header parameter.

message cannot be stolen as data sent is encrypted separately


2(a)
from i(i), it was mentioned that the attacker can modify the header of the data. as the header will contain data of the number of the attempts, mallory can modify the header to change the number of handshakes made from first to second


(b)
bob is still wrong as mallory can still sniff out all data being sent to alice as the man in the middle and modify all data sent back by the server to Alice, and change the reply message header from second to first



(c)
It can apply MAC using the secret key previously established
with Client. and sign the entire message


(d)
the update of TLS protocol willtake very long, so need to fix client application


--ans key--
. The GET command includes a value that is derived from
the cookie, e.g. MAC of the GET command and the
secret cookie, for Server’s verification.

can be done

(e)
by disabling renegotiation, it may the availablity of some websites, especially in cases where refreshes are needed, or a new connection need to be made due to a sudden crash of the previous session, which will necessitate the server to send over all information to the client again