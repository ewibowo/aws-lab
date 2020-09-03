
ASA Fundamentals
================

Security Level
--------------

From a higher security level to a lower security level:

* No ACL is required for traffic to traverse from a higher security level to a lower security level.
* The stateful inspection determines whether the return traffic is allowed to make it back through.

.. image:: ASA-security-level-high-to-low.png
   :width: 400px
   :alt: ASA Security Level: High to Low

From a lower security level to a higher security level:

* ACL is required for initiating traffic to traverse from a lower security level to a higher security level.
The ACL is usually applied (using access-group CLI) ingress on the interface with the lower security level (e.g. outside interface);
although it can also be applied egress on the interface with the higher security level (e.g. dmz interface).
* No ACL is required for the return traffic from a higher security level to a lower security level.

.. image:: ASA-security-level-low-to-high.png
   :width: 400px
   :alt: ASA Security Level: Low to High

Route Tables
------------

The management interface can be associated with its own management-only route table:

.. image:: ASA-management-only-RT.png
   :width: 400px
   :alt: ASA management-only Route Tables

Alternatively, the management interface can be associated with the main route table:

.. image:: ASA-main-route-table.png
   :width: 400px
   :alt: ASA main Route Tables