
vpc the network provided by AWS. using VPC the AWS resources can be access over the internet. by default one VPC is created by AWS of /16 CIDR
### subnets
by default there are subnets provided by AWS depending on the number of availability zone subnets are created. 5 ip are reserved 1 (network address),1(broadcast), 1(local router), 1(dns server), 1(future use)
network can be broken in the pieces knows as subnets.
## Route tables
to route the traffic the routing table is created. AWS by default creates the route table.
where a default route is present to forward traffic in local between subnets. 
and to enable internet the entry of internet gatway is present. (0.0.0.0/0) to IGW.
## Internet Gateway
Its user to provide internet to the EC2 computes. and attached to route tables depend on internet requirement.
## Network ACLs.
Network access control list is a security layer placed on the subnet layer which provide security over the subnet. both in and out rule needs to be specified to pass the desired traffic. its a 1st line of defense on network. rule are specified depend on number priority. lowest has higher priority and high has least priority. (1 to 100 or "\*")  keep spaces in priority no for best practice.
## Security Groups
sg is the security layer on the [[EC2 (Elastic Cloud compute)]] instance act as 2nd layer of security. and only provided security over ec2 instance. IN rule can be only need to allow for acces and the out/return traffic is automatic allowed.
![[Pasted image 20250114165007.png]]