## Nat Instance
Nat instance is used for network access translation. when we have 2 sub-nets in same [[VPC (virtual private cloud)]] of web-app and db then we don't want to give direct access of internet for db sub-net or server. 
so, the NAT instance server provide the internet using NAT software where the rule is written for forwarding traffic from private subnet [[EC2 (Elastic Cloud compute)]] instance to internet. 

![[Pasted image 20250116184010.png]]
## NAT Gateway

NAT gateway and NAT instance serves same purpose. but NAT gateway is the AWS inbuilt service where as NAT instance is the server with 3rd party software used for network translation. 

![[Pasted image 20250116183851.png]]