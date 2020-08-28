ASA
===============

This chapter discusses about how to deploy Cisco ASAv on AWS (Amazon Web Services). 

The primary ENI (elastic network interface) is mapped to the management interface (Management0/0) of ASA.
Windows bastion is deployed in a public subnet to be used for access the ASA management interface which is deployed in a private subnet.
.. image:: ASA-initial-topology.png
   :width: 600px
   :alt: ASA initial topology

Here is the topology of ASA on AWS VPC (virtual private cloud)
.. image:: ASA.png
   :width: 600px
   :alt: ASA

Several types of workload servers are placed in each subnet:

* Windows Bastion as a jump box 
* Ubuntu MGMT as a TFTP server 
* Ubuntu Client in inside (protected zone)
* Ubuntu Server in DMZ (de-militarised zone)

.. image:: ASA-Workload.png
   :width: 600px
   :alt: ASA
