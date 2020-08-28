ASA
===============

This chapter discusses about how to deploy ASAv on AWS. 

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
