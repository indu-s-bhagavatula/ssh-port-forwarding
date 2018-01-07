# ssh-port-forwarding
Demonstrate SSH Port forwarding using AWS EC2 instances

# CloudFormation Details 
Run the CloudFormation template VPC-SSH-PortForwarding-Demo to generate the VPC setup. The template will do the following: 
1. Create new VPC with CIDR 200.201.0.0/16
2. Creates a new InternetGateway and associate with the VPC. 
3. Creates a new EIP, NatGateway. NatGateway is associated with the EIP created. 
4. Create two subnets 
a. "ssh-port-forwarding-client-subnet" - 200.201.1.0/24 where the Bastion host will be deployed. This will be associated with the route table "ssh-port-forwarding-client-subnet-rt-tab". This is a route table that has 0.0.0.0/0 via IGW.
b. "ssh-port-forwarding-server-subnet" - 200.201.0.0/24 where the WebServer will be deployed. This will be associated with the route table "ssh-port-forwarding-server-subnet-rt-tab". This doesn't have a route via IGW and the subnet is Private. It has a route via a NatGatewway. 
5. Create two security groups: 
a. "ssh-port-forwarding-web-server-access-sg" contains rules to allow connectivity to the  Internal Web servery only from resources within the VPC. 
b. "ssh-port-forwarding-external-access-sg" contains rules that allow connectivity from External world.
