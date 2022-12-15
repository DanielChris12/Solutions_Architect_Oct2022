Task :  Create a dual Stack VPC and subnets using AWS CLI

Step:
1. Launch a non-default VPC
2. Create two subnets 
3. Create an internet gateway to one of the subnets with route table 
4. Configure an egress-only private subnet
5. Modify the IPv6 addressing behavior of the subnets
6. Lauch an instance into your public subnet
7. Launch an instance into your private subnet
8. Perform clean up operations. 


https://docs.aws.amazon.com/vpc/latest/userguide/vpc-subnets-commands-example.html

https://docs.aws.amazon.com/vpc/latest/userguide/vpc-subnets-commands-example-ipv6.html

https://docs.aws.amazon.com/vpc/index.html







## Task: Create a dual Stack VPC and subnets using AWS CLI

## 1. Launch a non-default VPC 

In the UI, go to 'Services'->'Network & Content Delivery' -> 'VPC' -> 'Your VPCs'. Select 'Create VPC'.

Let's call it "dualstack", give it a CIDR of your liking (let's say "10.10.0.0/24"), select "Amazon provided IPv6 CIDR block", and "Default" tenancy.

After creation of the VPC, select it and 'Enable DNS hostnames' and 'Enable DNS resolution'. (Note: DNS hostnames are only added with IPv4 addresses.

   OR
   
 Via the command-line, we'll use JSON output as the default (output = json in ~/.aws/config) and then utilize the versatile jq(1) command. To create the VPC, you'd then run
 
               $ export VPCID="$(aws ec2 create-vpc --cidr-block 10.10.0.0/24 --amazon-provided-ipv6-cidr-block | jq -r '.Vpc.VpcId')"
               $ aws ec2 create-tags --tags Key=Name,Value=dualstack --resources "vpc-0e6b37e0ef06f8675"
               $ aws ec2 modify-vpc-attribute --enable-dns-hostnames --vpc-id "vpc-0e6b37e0ef06f8675"
               $ aws ec2 modify-vpc-attribute --enable-dns-support --vpc-id "vpc-0e6b37e0ef06f8675"
               
Create an Internet gateway via the command line 

 
               $ aws ec2 create-internet-gateway
               $ aws ec2 create-tags --tags Key=Name,Value=dualstack --resources "igw-04ea78b51c9e52e8f"
               
 Then attach the gateway to the VPC
 
               $ aws ec2 attach-internet-gateway --vpc-id "vpc-0e6b37e0ef06f8675" --internet-gateway-id "igw-04ea78b51c9e52e8f"
               
 ## 2 Create two subnets 
 Via the command-line, we first need to determine the IPv6 CIDR associated with your VPC. AWS assigns a /56 by default, so we'll carve that up into a reasonably sized /64:
 
          $aws ec2 describe-vpcs --vpc-id "${VPCID}"
         $aws ec2 create-subnet --cidr-block 10.10.0.0/26 --ipv6-cidr-block ${V6CIDR%/56}/64 --vpc-id "${VPCID}"
         $ aws ec2 create-tags --tags Key=Name,Value=dualstack --resources "${SUBNET}"
         $ aws ec2 modify-subnet-attribute --subnet-id "${SUBNET}" --assign-ipv6-address-on-creation
         $ aws ec2 modify-subnet-attribute --subnet-id "${SUBNET}" --map-public-ip-on-launch
