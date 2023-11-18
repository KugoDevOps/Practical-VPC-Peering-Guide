# VPC_Peering
<div align="center">
  <strong><ins>Objective:</ins></strong>
  
<div align="left">
<strong><ins>Connecting VPCs:</ins></strong>
Allow communication between applications hosted in different VPCs by using VPC peering. The Marketing and Developer EC2 instances need to access the Financial Services server in the Finance department’s VPC.

<strong><ins>Solution Overview:</ins></strong> The solution is to make use of a separate virtual private cloud (VPC) for each department: Marketing, Developer, and Finance. 
The VPCs are connected by using VPC peering so that the resources in the Finance VPC are accessible to the Marketing and Developer VPCs. 

<image sr="https://imgur.com/FLhVhuP"><img src="https://i.imgur.com/FLhVhuP.png" title="source: imgur.com">


| VPC  | Marketing VPC |                            
|---|---|
| CIDR Block | 10.0.0.0/16 |
| Target | 172.31.0.0/16 |

| VPC  | Developer VPC|                            
|---|---|
| CIDR Block | 192.168.0.0/20 |
| Target | 172.31.0.0/16 |

| VPC  | Finance VPC|                            
|---|---|
| CIDR Block | 172.31.0.0/16 |

<strong><ins>Explore VPCs:</ins></strong>

By default, VPCs are isolated from each other. A VPC peering connection is a networking connection between two VPCs that you can use to route traffic between them by using their private IP addresses. 

<a href="https://imgur.com/bBSKREs"><img src="https://i.imgur.com/bBSKREs.gif" title="source: imgur.com">

There are 3 instances all assigned to a separate department: Marketing, Finance and developer. The Private IPv4 address **(172.31.1.199)** of the FinanceServer Instance is selected and copied.


The Marketing EC2 instance is connected via the **Session Manager**. From the session manager, the Marketing Instance tries to connect to the FinanceServer Instance but the connection fails. 

<a href="https://imgur.com/cIM231S"><img src="https://i.imgur.com/cIM231S.gif" title="source: imgur.com" /></a>


The connection is unsuccessful because VPCs cannot communicate with resources in other VPCs using IPv4 and IPv6 addresses. 

A peering connection is needed to establish communication between VPCs. **A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them privately**.

<a href="https://imgur.com/0bQ1G5R"><img src="https://i.imgur.com/0bQ1G5R.png" title="source: imgur.com" /></a>


<a href="https://imgur.com/wcIGjg7"><img src="https://i.imgur.com/wcIGjg7.gif" title="source: imgur.com" /></a>

After establishing a peering connection, the route table must be modified to show the association in the VPCs. A route must be added to each route table to allow traffic between the peered VPCs. 

**Marketing EC2 Instance Route**:
<a href="https://imgur.com/4QBNG5n"><img src="https://i.imgur.com/4QBNG5n.gif" title="source: imgur.com" /></a>

**Finance EC2 Instance Route:**
<a href="https://imgur.com/TKPSPDq"><img src="https://i.imgur.com/TKPSPDq.gif" title="source: imgur.com" /></a>

The Marketing EC2 instance is connected via the Session Manager. From the **session manager**, the Marketing Instance tries to connect to the FinanceServer Instance but the connection fails again. 
<a href="https://imgur.com/4dpX0XM"><img src="https://i.imgur.com/4dpX0XM.gif" title="source: imgur.com" /></a>

Peered VPCs do not automatically accept all data between them. Security features such as network ACLs and Security Groups still apply restrictions and access to the VPC. 	
After modifying the security group rule: 
<a href="https://imgur.com/JdS3OQa"><img src="https://i.imgur.com/JdS3OQa.gif" title="source: imgur.com" /></a>

**The VPCs can finally communicate:**
<a href="https://imgur.com/aZRTNs1"><img src="https://i.imgur.com/aZRTNs1.gif" title="source: imgur.com" /></a>

_A peering connection is finally established between the Marketing VPC and the Finance VPC. Next, we repeat same steps and connect the Developer VPC to the finance VPC._


