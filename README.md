# VPC_exercise

#Objective
Connecting VPCs: Allow communication between applications hosted in different VPCs by using VPC peering. The Marketing and Developer EC2 instances need to access the Financial Services server in the Finance department’s VPC.

#Solution Overview
The solution is to make use of a separate virtual private cloud (VPC) for each department: Marketing, Developer, and Finance. The VPCs are connected by using VPC peering so that the resources in the Finance VPC are accessible to the Marketing and Developer VPCs. 


