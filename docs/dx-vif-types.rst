Public Virtual Interfaces
=========================
Allow a customer to connect to AWS public endpoints and services such as (S3, Glacier, Cloud Front and SES endpoints) as well as resources in AWS that are accessible via Public IPs such as Internet-facing ELB and EC2.

Private Virtual Interfaces
==========================
Allow a customer to connect to resources inside one or more VPCs such as EC2, ELB, RDS using their private IP addresses.

Transit Virtual Interfaces
==========================
Allow a customer to conenct to a Transit Gateway.

It is important to note that you cannot use a Public VIF to access VPC resources using Private IP. However, you will be able to access EC2 using Public IP using Direct Connect VIF. In addition, it is not possible to connect directly to the Internet using Direct Connect. 