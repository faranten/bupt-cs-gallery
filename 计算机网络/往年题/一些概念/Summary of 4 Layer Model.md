2022/3/6

# Summary of 4 Layer Model

rongtianfu@gmail.com

Stanford University

## Application: Application(e.g. http) and Presentation(e.g. ASCII)

​	Bi-directional reliable bytes stream between two applications, using application-specific semantics (e.g. http, bit-torrent).

## Transport: Transport and Session

​	Guarantees correct, in-order delivery of data end-to-end. Control congestion.

## Network: Network

​	Delivers datagram end-to-end. Best-effort delivery-no guarantees. Must use the Internet Protocol (IP).

## Link: Link and Physical

​	Delivers data over a single link between an end host and router, or between routers



## IP is the "thin waist"

1. http, smtp, ssh, ftp, ...
2. TCP, UDP, RTP, ...
3. IP
4. Ethernet, WiFi, DSL, 3G, ...