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

then i created a public route table , public route and then associated the public route table to the piublic subnet 1 and 2..... 
When editing the route open the destination to 0.0.0/0 and the target to the internet gateway i created 

Note: The major the difference between a public and private subnet is that a public subnet has an internet gatway attached to its route table.






For guide, you are check the links below:

https://docs.aws.amazon.com/cli/latest/reference/ec2/

https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-vpcs.html

