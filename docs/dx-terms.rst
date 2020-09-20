Direct Connect Termininologies
==============================

Direct Connect Locations
------------------------
These are the physical data centers where AWS has its Point of Presence for Customers to enable connectivity to the geographically nearest AWS region.

COLO
----
A colocation (colo) is a Data Center Facility where equipment, space and bandwidth are available for rental to reatil customers. Colocation facilities provide space, power, cooling and physical security for the server, storage and networking equipment of other firms and connect them to a variety of telecommunications and network service providers with a minimum of cost and complexity. 

Single Mode fiber
-----------------
Single mode fiber optic cable has a small diameter core that allows only one mode of light to propagate. Single mode fiber optic cable is used for long-distance communication.

Border Gateway Protocol
-----------------------
BGP is a standarised exterior gateway protocol designed to exchange routing and reachability information among Autonoumous Systems (AS) on the Internet. In BGP, there is a peering relationship between 2 peers. Traffic that is routed within single network AS is referred to as internal BGP or iBGP. More often BGP is used to connect one AS to other autonomous systems and it is then referred to as External BGP or eBGP.

VLAN
----
Virtual Local Area Network which helps to isolate/partition networks from each other at Layer 2.

802.1Q
------
It is the network standard protocol that supports VLAN on an Ethernet network.

MD5
---
MD5 authentication is mechanism used to verify BGP peer relationship. Both peers need to have the same password in order to communiate with each other.

LOA-CFA
-------
Letter of Authorisation and Connecting Facility Assignment is an authorisation document which customer is able to provide to the COLO facility to create a hardwired connection between Customer network and AWS.

MMR
---
Meet Me Room is the common room where AWS has its demarcation point for and will have the ports available on the patch panel for the customer to connect into.

A Side
------
From the customer perspective, this is the customer provider side of the patch panel in the MMR.

Z Side 
------
From the customer perspective, this is the AWS side of the patch panel in the MMR.

Cross-Connect
-------------
It is any connection between facilities provided as separate units by the datacenter. The line that runs from Customer to the AWS rack is a cross-connect.

SFP
---
Small Form-factor Pluggable (SFP) is a compact, hot - pluggable transceiver used on both side of the fiber cable. 

Loopback Tester
---------------
A device that can be inserted into an SFP or patch pannel port to determine if a physical port or segment of fiber optic cabling is functioning properly. This device creates a physical loop on the SFP or cable, effectively testing both the transmit (Tx) and receive (Rx) strands. 