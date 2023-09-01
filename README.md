

# classic-3-tier-app-on-aws
Classic Three Tier Application running on AWS: Public Tier (Load-Balancer/Proxy), Application Tier, Database Tier

### AWS Featured Resources - VPC, Rout 53, RDS, Application LoadBalancer, EC2

### A Network topology for this App to run is essential.
Create a VPC with a 10.0.0.0/21 IPV4 Cidr Range (2046 IP Addresses) and enable AWS-provided IPv6

![Create VPC](./assets/Create3tierVPC.png)

Create Subnets Per Tier Per AZ to achieve HA, Fault-Tolerance & Isolation

![Create Subnet Per Tier Per AZ](./assets/SubnetPerTierPerAZ.png)

### Internet Access
By Default, VPCs are private & don't communicate with the outside world. An Internet Gateway(IGW) is required for a VPC to access the Internet & The public subnets that require access to the Internet are explicitly associated with Route Tables which have routes to the IGW

### Create an IGW - Attach to the VPC - then use the IGW as a Target for Routes

![Create IGW](./assets/3-Tier-App-IGW.png)

### Private Subnets Sometimes need One-way communication to the internet, NAT enables this for IPv4 traffic & Egress-Only Internet Gateway enables this for IPv6 traffic.

### Create NAT in a Public Subnet with an Elastic Public IP Attached

![Create NAT](./assets/CreateNAT.png)

### Egress-Only Internet Gateway - For egress-only traffic for IPv6

![Create EIGW](./assets/3-tier-app-eigw.png)



### Configure Routing
Routing is only concerned with whether traffic can flow from one place to another. Routing is not concerned with protocols e.g. TCP/UDP/ICMP, nor concerned with ports e.g. 80/443

***All VPCs have a default route table, with default routes & this is referred to as the "Main Route Table" If a Subnet is not explicitly associated with a route table, it is implicitly associated with the main route table***

### Create Route Tables

