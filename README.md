# VPC-with-servers-in-private-subnets-and-NAT

# About the Project-

This project demonstrates how to create a VPC that you can use for servers in a production enviornment.
To improve resiliency, you deploy the servers in two Available Zones, by using an Auto Scaling group and an Load Balancer.For additional securitry, you deploy the servers in private subnets. The servers receive 
request through the load balancer. The servers can connect to the internet by using a NAT gateway. To improve resiliency, you deploy the NAT gateway in both Availability Zones.

# Overview-
The VPC has public subnets and private subnets in two Availability Zones.
Each public subnet contains a NAT gateways and a load balancer node.
The servers run in the private subnets, are launched and terminated by using an Auto Scaling group, and receive traffic from the load balancer.
The servers can connect to the internet by using the NAT gateway.

![vpc-example-private-subnets](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/198acfe8-25b3-4079-9188-aa60a6b9439a)

- Design and configure a VPC: Create a VPC with custom IP ranges. Set up public and private subnets. Configure route tables and associate subnets.
- Implement network security: Set up network access control lists (ACLs) to control inbound and outbound traffic. Configure security groups for EC2 instances to allow specific ports and protocols.
- Provision EC2 instances: Launch EC2 instances in both the public and private subnets. Configure security groups for the instances to allow necessary traffic. Create and assign IAM roles to the instances with appropriate permissions.
- Networking and routing: Set up an internet gateway to allow internet access for instances in the public subnet. Configure NAT gateway or NAT instance to enable outbound internet access for instances in the private subnet. Create appropriate route tables and associate them with the subnets.
- SSH key pair and access control: Generate an SSH key pair and securely store the private key. Configure the instances to allow SSH access only with the generated key pair. Implement IAM policies and roles to control access and permissions to AWS resources.
- Test and validate the setup: SSH into the EC2 instances using the private key and verify connectivity. Test network connectivity between instances in different subnets. Validate security group rules and network ACL settings

By implementing this project, I've gained hands-on experience in setting up a secure VPC with EC2 instances, implementing networking and routing, configuring security groups and IAM roles, and ensuring proper access control. This project will provide a practical understanding of how these AWS services work together to create a secure and scalable infrastructure for applications.

![Screenshot 2024-01-17 221659](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/c1bc026e-0a15-4084-880c-afd5ee4ce16c)


![Screenshot 2024-01-19 132524](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/5a44f250-10e0-4b38-977d-0ca593cb85b7)


![Screenshot 2024-01-19 132126](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/f90e0bee-b590-4f83-8ba5-55d3d3f0bdda)


![Screenshot 2024-01-17 224523](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/7dfd73d7-316e-4709-8529-ac0643803bc5)








