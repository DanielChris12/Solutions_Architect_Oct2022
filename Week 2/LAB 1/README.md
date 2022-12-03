This task will get you acquainted on how to deploy VPC 


Task 1: Deploy VPC using Management console
1. Launch the AWS Management Console
2. Launch a VPC with one public and one private subnets.
3. Create two route table and associate  each one to each subnets
4. Attach an internet gateway to the VPC and a NAT gateway to the private subnet.
5. Lauch a Linux instance into this VPC and attach the subnet
6. Test the network connectivity
7. Perform clean up actions














## 1. Launch the AWS Management Console

I logged in unto my management console by using my user id and providing the MFA code for security reasons 

## 2. Launch a VPC with one public sand one private subnets

To achieving this i followed this steps ;
  
  Firstly, i choose my region.Then,clicked on the service icon and then seacrh for VPC which i clicked on when it popped up. Then clicked on create VPC and i created one , i discovered after creating the VPC it automatically created a route table that is private. Then, i created an internet gateway and attach the internet gateway to the VPC i created.(so that the instances of our subnet can have access to the internet)
  
  Note: You can only attach one internet gateway to a VPC

After attaching the internet gateway i created a subnet and attached it to the my created VPC, Then i enable automatic assigning of IPV4 addresses.

## 3. Create two route table and associate  each one to each subnets

Then i created two route table with name public and private route table , public route and then associated the public route table to the piublic subnet 1 and 2..... 

## 4.  Attach an internet gateway to the VPC and a NAT gateway to the private subnet.

When editing the route open the destination to 0.0.0/0 and the target to the internet gateway i created 

Note: The major the difference between a public and private subnet is that a public subnet has an internet gatway attached to its route table.

To create a NAT gateway for my private subnet i had to allocate and elastic ip address to the private subnet created afterwards i webt to edit my route table by opening the destination to 0.0.0/0 and the target to the NAT gateway i created 

## 5. Launch a Linux instance into this VPC and attach the subnet

Click on the service icon the look for security, identity an compliance -- i clicked on IAM to create a role under select trusted identity-- select AWS services and then EC2 and then click on next permission. Under policy name select amazonEC2SSM and name the role SSMRole then clicked on next to create the role

Afterwards, we would launch an EC2 instance in any of the subnet created and attach the SSMRole --- To do that go to service click on EC2  under network select the created VPC and subnet too and attach the SSM Role to it then launch instance 


## 6. Test the network connectivity

Use the run command to test if the EC2 has an outbound internet access through the NAT Gateway --- select the service icon search for system manager then select run command and select run shellscript and then ran sudo yum update-y 

And then select the the EC2 instance 



## HERE ARE SOME SCREENSHOT

<img width="1436" alt="Screenshot 2022-11-29 at 18 32 32" src="https://user-images.githubusercontent.com/105374941/205440433-8116a7d6-646e-4f77-84ef-b1660bd64ba0.png">

<img width="1249" alt="Screenshot 2022-12-01 at 11 54 19" src="https://user-images.githubusercontent.com/105374941/205440439-262a9052-f862-4284-973b-9a2c54bae21a.png">

<img width="1249" alt="Screenshot 2022-12-01 at 11 55 03" src="https://user-images.githubusercontent.com/105374941/205440443-f9882f8f-7df8-4ad0-92cf-63fb8977d505.png">

<img width="1427" alt="Screenshot 2022-12-01 at 12 04 02" src="https://user-images.githubusercontent.com/105374941/205440471-42aea2a1-9dd3-4a9d-b018-adc11b9537cb.png">


<img width="1427" alt="Screenshot 2022-12-01 at 12 21 44" src="https://user-images.githubusercontent.com/105374941/205440475-07163c8a-1681-4e59-8afe-2f3f7b9ca223.png">


<img width="1427" alt="Screenshot 2022-12-01 at 12 31 06" src="https://user-images.githubusercontent.com/105374941/205440493-4cef374e-0df7-412e-9815-f013e1d217b8.png">


<img width="1427" alt="Screenshot 2022-12-03 at 12 31 07" src="https://user-images.githubusercontent.com/105374941/205440527-ed68a46b-7a95-405e-aae9-87954ef90a14.png">


<img width="1427" alt="Screenshot 2022-12-03 at 12 24 10" src="https://user-images.githubusercontent.com/105374941/205440528-fe390230-6836-4030-a191-44fef5b81d7e.png">


<img width="1427" alt="Screenshot 2022-12-03 at 12 57 09" src="https://user-images.githubusercontent.com/105374941/205440558-5e99aa49-4002-4e7a-88d8-fe30ada05092.png">

<img width="1427" alt="Screenshot 2022-12-03 at 12 56 25" src="https://user-images.githubusercontent.com/105374941/205440563-a7d73fac-2d72-449d-90cb-cb7b716a1ce1.png">

<img width="1427" alt="Screenshot 2022-12-03 at 13 00 45" src="https://user-images.githubusercontent.com/105374941/205440566-511a24f0-b44c-4a2b-932c-dfb95b0d5253.png">


For guide, you are check the links below:

https://docs.aws.amazon.com/cli/latest/reference/ec2/

https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-vpcs.html

