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

1. Now you have to choose the Key-pair you created.

![Screenshot 2024-01-20 183617](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/66112ff9-f1de-4c26-82da-31a5610eaeb8)


![Screenshot 2024-01-20 183652](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/97ff6f2d-3781-42be-9d50-603f41a683cd)


![Screenshot 2024-01-20 183728](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/7c5f95de-0cc1-40cb-89cc-97faf730e7a6)


![Screenshot 2024-01-20 183747](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/63bfb395-cccd-4e4d-8213-6dbb38919207)

2. Scroll Down and then Click "Next".

![Screenshot 2024-01-20 183815](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/9c51dd37-cc2d-4fe7-98b2-976620d9a347)

3. Scroll Down and then Click "Next".

![Screenshot 2024-01-20 184311](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/c5d61650-2873-404b-aea1-a83be0d05428)

4. Scroll Down and then Click "Next".

![Screenshot 2024-01-20 184349](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/2509fffb-9733-44e9-8042-2de979efa0b5)

5. Scroll Down and then Click "Skip to Review".

![Screenshot 2024-01-20 184421](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/db85c4cd-4497-4535-96fb-638fe3607541)

6. Now your are Successfully Created Auto Scaling Group.
7. Open the AWS Management Console.
8. Navigate to the EC2 console by clicking on "Services" in the top-left corner, then selecting "EC2" under the "Compute" section.
9. In the EC2 dashboard, you'll find the "Instances" link on the left-hand navigation pane. Click on "Instances."
10. Here, you should see the list of EC2 instances associated with your account. Look for the instances created by your Auto Scaling Group.
Since you mentioned that the Auto Scaling Group launched instances in different AZs, you can check the "Availability Zone" column to verify that these instances are indeed distributed across multiple AZs.

# Step 3 :
Creating the Bastion Host :
1. Launch Instance as Specified below .

![Screenshot 2024-01-20 184453](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/0a5a9c55-7954-4e2d-8904-501d13cd7b25)


![Screenshot 2024-01-20 184526](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/d5a8e8c8-d01b-4785-9304-e3303fd1633c)


![Screenshot 2024-01-20 184600](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/f1c80493-f68b-4f39-8e67-d190e119f067)


![Screenshot 2024-01-20 184642](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/7d4486e0-47a8-46a4-87e0-a27b8a3c5e50)


![Screenshot 2024-01-20 184721](https://github.com/shamshad74/VPC-with-servers-in-private-subnets-and-NAT/assets/117065471/b955daf5-eeaa-4f64-a9c5-a25f3ec56942)

# Step 4:
SSH into Private Instance
1. SSH into the Bastion Host Instance: To SSH into the private instances, we first need to connect to our Bastion host instance. From there, we'll be able to SSH into the private instance.
2. Ensure the PEM File is Present on the Bastion Host: Additionally, make sure that the PEM file is present on the Bastion host. Without it, you won't be able to SSH into the private instance from the Bastion host.
3. Open a Terminal: Open a terminal window on your local machine.
4. Execute the Following Commands:
   - If your PEM file is named something like <aws demo.pem>, you must remove spaces in the filename. Please rename the file to something like <aws_demo.pem>.
   -  Copy the PEM file to the Bastion host using the scp command. Replace <pem file location> with the local and remote file paths, and <bastion host public IP> with the Bastion host's public IP address.
      Example:                                                                                                         
      scp -i /Users/mathesh/Downloads/aws_demo.pem /Users/mathesh/Downloads/aws_demo.pem ubuntu@34.229.240.123:/home/ubuntu
   - The above command will copy the PEM file from your computer to the Bastion host. Once the file is successfully copied, move on to the next step. d. SSH into the Bastion host using the following command:                                        
      ssh -i aws_demo.pem ubuntu@34.229.240.123











