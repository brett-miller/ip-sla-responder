Cisco IP-SLA / Juniper RPM responder
====================================

Contents
--------

1. About
2. Warnings
3. Installation
4. Usage
5. TODO

Please visit http://cmouse.github.com/ip-sla-responder/ for latest information. 

About
-----

This program is intended for Cisco IP-SLA and Juniper PRM measurements. You can configure it to listen on any ethernet interface, and it'll reply to you. It expects all packets to be 802.1q encapsulated, and it works best if you do not configure any vlans into your system. IP and MAC address can be freely chosen, and do not need to be configured on your system. It supports both IPv4 and IPv6 protocols. You can also run it for your own measurement systems by utilizing the UDP ECHO port, it'll reply to you whatever you send there.

Warnings
--------
Note that this software has absolutely no rate limiting. If you put it on a machine, it *will* reply as fast as possible. It has no DDoS protection or any kind of access lists. You can easily ping someone to death with it. Be careful and use ACLs in front of it. 

Installation
------------

To install, run make CC=gcc (or some other compiler, default is cc). This software expects linux 2.6 or better kernel, or kernel with similar facilities. It needs pcap(3) interface on kernel and AF_PACKET. It also requires librt and libpcap. 

Usage
-----

The software can run in either routed or connected mode. In routed mode, you are expected to route in some IP via some VLAN. You can disable VLAN support in config file if necessary. In connected mode, you can have one or more vlans configured with same network on the network side, and nothing on linux side. Best if you don't configure any vlans and leave the interface offline, so linux or the nic won't eat up your packets. This is best used if you want to support same IP address on multiple VRFs. You can use up to 4096 different VLANs. 

To configure the software, copy and edit responder.conf.sample. Program accepts
one parameter, location where to read the file. Default is /etc/responder.conf
or whatever you defined in Makefile.

After this, you can point Cisco IP SLA UDP echo, UDP Jitter measurements (udp-jitter), or Juniper RPM icmp-ping(-timestamp) or udp-ping(-timestamp) measurements towards the IP. It'll reply these.

TODO
----

 * Add more supported types for Cisco
 * Daemonize?
 * Code cleanup and documentation
