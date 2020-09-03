
ASA Fundamentals
================

ASA in Cisco ASA stands for Adaptive Security Appliance.

Cisco ASA is a  security device that combines firewall, antivirus, intrusion prevention, and virtual private network (VPN) capabilities.  

Security Level
--------------

Each ASA interface must have ip address, security-level and nameif configured to work. Security levels are numbered from 0 to 100. 

From a higher security level to a lower security level:

* ACL (access control list) is not required for traffic to traverse from a higher security level to a lower security level.
* The stateful inspection determines whether the return traffic is allowed to make it back through.

.. image:: ASA-security-level-high-to-low.png
   :width: 400px
   :alt: ASA Security Level: High to Low

From a lower security level to a higher security level:

* ACL is required for initiating traffic to traverse from a lower security level to a higher security level. The ACL is usually applied (using access-group CLI) ingress on the interface with the lower security level (e.g. outside interface); although it can also be applied egress on the interface with the higher security level (e.g. dmz interface).
* No ACL is required for the return traffic from a higher security level to a lower security level.

.. image:: ASA-security-level-low-to-high.png
   :width: 400px
   :alt: ASA Security Level: Low to High

Route Tables
------------

The management interface can be associated with its own management-only route table:

.. image:: ASA-management-only-RT.png
   :width: 600px
   :alt: ASA management-only Route Tables

Alternatively, the management interface can be associated with the main route table:

.. image:: ASA-main-route-table.png
   :width: 600px
   :alt: ASA main Route Tables

Next step, let us deploy virtualised Cisco ASA (ASAv) in Amazon Web Services cloud.