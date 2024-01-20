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


# STEPS:

# step 1
# Create The VPC
1. Open the Amazon VPC console
2. On the dashboard, click on "Create VPC"
3. Under "Resources to create," select "VPC and more"
4. Configure the VPC:
    - Provide a name for the VPC in the "Name tag auto-generation" field
    - For the IPv4 CIDR block, leave it as default suggestion
5. Configure the subnets:
    - Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones
    - Specify the "Number of public subnets" as 2
    - Specify the "Number of private subnets" as 2
    - For NAT gateways, choose "1 per AZ" to enhance resiliency
    - For VPC endpoints, you can choose "None"
    - Regarding DNS options, clear the checkbox for "Enable DNS hostnames"
    - Once you've configured all the settings, click "Create VPC"

6. Now you can see you are successfully Created VPC .

![Screenshot 2024-01-17 221659](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/c1bc026e-0a15-4084-880c-afd5ee4ce16c)


![Screenshot 2024-01-19 132524](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/5a44f250-10e0-4b38-977d-0ca593cb85b7)


![Screenshot 2024-01-19 132126](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/f90e0bee-b590-4f83-8ba5-55d3d3f0bdda)


![Screenshot 2024-01-17 224523](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/7dfd73d7-316e-4709-8529-ac0643803bc5)


# Step 2
# Creating the Auto Scaling Group :


![Screenshot 2024-01-19 140313](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/3c9b27f4-d2c2-49f7-ac5f-e305b347f19e)


![Screenshot 2024-01-19 140339](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/aaf74615-2311-4a63-8d92-44201d7c0017)


![Screenshot 2024-01-19 140359](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/ab4ddfb1-001e-4fc1-91a6-c2360270c828)


![Screenshot 2024-01-19 140429](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/3396d6f0-fd46-4396-8d95-d8850e2e932a)


![Screenshot 2024-01-19 140451](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/e153c348-ceeb-4350-9690-9360428bcbf1)


![Screenshot 2024-01-19 140513](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/e99759c8-d4ea-4454-b83e-8ab53d919ce9)


![Screenshot 2024-01-20 183617](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/66112ff9-f1de-4c26-82da-31a5610eaeb8)


![Screenshot 2024-01-20 183652](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/97ff6f2d-3781-42be-9d50-603f41a683cd)


![Screenshot 2024-01-20 183728](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/7c5f95de-0cc1-40cb-89cc-97faf730e7a6)


![Screenshot 2024-01-20 183747](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/63bfb395-cccd-4e4d-8213-6dbb38919207)


![Screenshot 2024-01-20 183815](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/9c51dd37-cc2d-4fe7-98b2-976620d9a347)










