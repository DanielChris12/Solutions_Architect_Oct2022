Task: Create a nondefault VPC using AWS CLI

1. Open your CLI and run a configuration setting
2. Lauch a VPC 
3. Create two subnets (a public and a private subnet)
4. Make your subnet public by creating and attaching an internet gateway
5. Create a security group and add a SSH access from anywhere
6. Lauch an instance into your subnet 
7. Clean Up

https://docs.aws.amazon.com/vpc/latest/userguide/vpc-subnets-commands-example.html

https://docs.aws.amazon.com/vpc/latest/userguide/vpc-subnets-commands-example-ipv6.html

https://docs.aws.amazon.com/vpc/index.html







## 1. Open your CLI and run a configuration setting 

The following example uses AWS CLI commands to create a nondefault VPC with an IPv4 CIDR block, and a public and private subnet in the VPC

## 2.Launch a VPC

The first step is to create a VPC and two subnets. The CIDR block 10.0.0.0/16 for the VPC, but you can choose a different CIDR block

aws ec2 create-vpc --cidr-block 10.0.0.0/16

## 3. Create two public subnets ( a public and a private subnet)

Using the VPC ID from the previous step, create a subnet with a 10.0.1.0/24 CIDR block

aws ec2 create-subnet --vpc-id vpc-049f6eea2c398e7c4, --cidr-block 10.0.1.0/24

## 4. Make your subnet public by creating and attaching an internetgateway

After we’ve created the VPC and subnets, we can make one of the subnets a public subnet by attaching an Internet gateway to our VPC, creating a custom route table, and configuring routing for the subnet to the Internet gateway.

aws ec2 create-internet-gateway

Using the ID from the previous step, attach the Internet gateway to your VPC.

aws ec2 attach-internet-gateway --vpc-id "vpc-049f6eea2c398e7c4",  --internet-gateway-id  "igw-0cc8164aea1d14a4d",

Create a custom route table for our VPC

aws ec2 create-route-table --vpc-id "vpc-049f6eea2c398e7c4"

In the output that’s returned, take note of the route table ID. In the output that’s returned, take note of the route table ID.

aws ec2 create-route --route-table-id "rtb-0c0b5429a73a3136e" --destination-cidr-block 0.0.0.0/0 --gateway-id "igw-0cc8164aea1d14a4d",

## 5. Create a security group and add a SSH access from anywhere.

## 6.  Lauch an instance into your subnet

## Here are Some Screenshot



![CLI VPC 02](https://user-images.githubusercontent.com/105374941/207685948-98a59ef9-ae4e-4dc9-93de-b36b5aa37d38.png)

