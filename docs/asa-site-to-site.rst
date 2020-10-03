Site to Site VPN 
================

In this chapter, we will configure a IPsec tunnel between ASAv and AWS Managed VPN: 

.. image:: ASAv-Site-to-Site-VPN.png
   :width: 600px
   :alt: Site to Site VPN - IPsec

First of all, let's prepare the AWS Managed VPN:

#. Create a VGW (Virtual Private Gateway).
#. Attach the newly created VGW to a VPC.
#. Create a VPN connection and attach it to the newly created VGW.
#. Enable the route propagation from VGW to the subnet route table.

Create a VGW (Virtual Private Gateway):

Now, we are ready to configure our ASAv to connect the AWS managed VPN.

ASAv configuration:

.. code-block:: console

    ! --------------------------------------------------------------------------------
    ! IPSec Tunnel #1
    ! --------------------------------------------------------------------------------
    ! #1: Internet Key Exchange (IKE) Configuration

    crypto ikev1 enable outside 

    crypto ikev1 policy 200
    encryption aes 
    authentication pre-share
    group 2
    lifetime 28800
    hash sha

    ! --------------------------------------------------------------------------------		
    ! #2: IPSec Configuration

    crypto ipsec ikev1 transform-set ipsec-prop-vpn-04a0ce01a40f54075-0 esp-aes  esp-sha-hmac


    ! The IPSec profile references the IPSec transform set and further defines
    ! the Diffie-Hellman group and security association lifetime.
    crypto ipsec profile ipsec-vpn-04a0ce01a40f54075-0
    set pfs group2
    set security-association lifetime seconds 3600
    set ikev1 transform-set ipsec-prop-vpn-04a0ce01a40f54075-0
    exit

    ! This option instructs the router to clear the "Don't Fragment"
    ! bit from packets that carry this bit and yet must be fragmented, enabling
    ! them to be fragmented. 
    crypto ipsec df-bit clear-df outside

    ! This option causes the firewall to reduce the Maximum Segment Size of
    ! TCP packets to prevent packet fragmentation.
    sysopt connection tcpmss 1379

    ! This configures the gateway's window for accepting out of order
    ! IPSec packets. A larger window can be helpful if too many packets
    ! are dropped due to reordering while in transit between gateways.
    crypto ipsec security-association replay window-size 128

    ! This option instructs the router to fragment the unencrypted packets
    ! (prior to encryption).
    crypto ipsec fragmentation before-encryption outside

    ! The tunnel group sets the Pre Shared Key used to authenticate the 
    ! tunnel endpoints.
    tunnel-group 13.54.44.222 type ipsec-l2l
    tunnel-group 13.54.44.222 ipsec-attributes
    ikev1 pre-shared-key <your-pre-shared-key>

    ! This option enables IPSec Dead Peer Detection, which causes semi-periodic
    ! messages to be sent to ensure a Security Association remains operational.

    isakmp keepalive threshold 10 retry 10
    exit

    ! --------------------------------------------------------------------------------
    ! #3: Tunnel Interface Configuration

    ! Association with the IPSec security association is done through the
    ! "tunnel protection" command.
    interface Tunnel1
    nameif Tunnel-int-vpn-04a0ce01a40f54075-0		
    ip address 169.254.179.162 255.255.255.252
    tunnel source interface outside
    tunnel destination 13.54.44.222
    tunnel mode ipsec ipv4
    tunnel protection ipsec profile ipsec-vpn-04a0ce01a40f54075-0
    no shutdown
    exit

    ! --------------------------------------------------------------------------------
    ! #4: Border Gateway Protocol (BGP) Configuration

    router bgp 64513
    address-family ipv4 unicast
        neighbor 169.254.179.161 remote-as 64512
        neighbor 169.254.179.161 timers 10 30 30
        neighbor 169.254.179.161 default-originate
        neighbor 169.254.179.161 activate
        
    ! To advertise additional prefixes to Amazon VPC, copy the 'network' statement
    ! and identify the prefix you wish to advertise. Make sure the prefix is present
    ! in the routing table of the device with a valid next-hop.
    ! network 0.0.0.0 
        network 172.16.2.0 mask 255.255.255.0
        no auto-summary
        no synchronization
    exit-address-family
    exit

Route table on ASAv:

.. code-block:: console

ciscoasa# show route

Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, V - VPN
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, + - replicated route
       SI - Static InterVRF
Gateway of last resort is 172.16.1.1 to network 0.0.0.0

S*       0.0.0.0 0.0.0.0 [1/0] via 172.16.1.1, outside
B        10.0.0.0 255.255.0.0 [20/100] via 169.254.179.161, 00:21:10
C        169.254.179.160 255.255.255.252
           is directly connected, Tunnel-int-vpn-04a0ce01a40f54075-0
L        169.254.179.162 255.255.255.255
           is directly connected, Tunnel-int-vpn-04a0ce01a40f54075-0
C        172.16.1.0 255.255.255.0 is directly connected, outside
L        172.16.1.254 255.255.255.255 is directly connected, outside
C        172.16.2.0 255.255.255.0 is directly connected, inside
L        172.16.2.254 255.255.255.255 is directly connected, inside
C        172.16.3.0 255.255.255.0 is directly connected, dmz
L        172.16.3.254 255.255.255.255 is directly connected, dmz


Ping from Ubuntu client:

.. code-block:: console

    ubuntu@ip-172-16-2-100:~$ ping 10.0.2.14
    PING 10.0.2.14 (10.0.2.14) 56(84) bytes of data.
    64 bytes from 10.0.2.14: icmp_seq=52 ttl=63 time=94.6 ms
    64 bytes from 10.0.2.14: icmp_seq=53 ttl=63 time=95.8 ms
    64 bytes from 10.0.2.14: icmp_seq=54 ttl=63 time=96.2 ms
    64 bytes from 10.0.2.14: icmp_seq=55 ttl=63 time=95.4 ms
    64 bytes from 10.0.2.14: icmp_seq=56 ttl=63 time=95.1 ms