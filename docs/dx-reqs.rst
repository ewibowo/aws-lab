Direct Connect Requirements
===========================
Customer router should be one of the DX colocations. If not, then the customer can work with an APN or Service Provider to get their Data Center connected to AWS using Direct Connect.

Conditions
==========
- Use single mode fiber
- 1000Base-LX (1310nm) transceiver for 1 Gigabit Ethernet or 10GBASE-LR (1310nm) tansceriver for 10 Gigabit Ethernet. 
- Disable auto-negotiation
- Support 802.1Q VLAN
- Support BGP with MD5 authentication
- Routes per BGP session on a privage VIF is 100
- Routes per BGP session on a public VIF is 1000