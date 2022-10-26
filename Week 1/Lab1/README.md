This Week lab will focus on getting you acquainted with Amazon S3 using the aws cli

# Task 1: Create a S3 bucket using AWS CLI

1. Lauch AWS cloud shell
2. Create a S3 bucket 
3. Create a folder in your S3 bucket
4. Upload objects to your S3 bucket
5. List the object in your S3 bucket
6. Download Object from your S3 bucket
7. Delete object in your s3 bucket
8. Delete your S3 bucket





For guide, kindly visit

https://docs.aws.amazon.com/cli/latest/reference/s3api/create-bucket.html

https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html

https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html







## My LAB Experience 

## Task 1: Create a S3 bucket using AWS CLI


## 1. Lauch AWS cloud shell
Go to the AWS sign console.When you at the portal interface go to the notification bars and click on the first box from your right. Clicking on that will launch the AWS Cloud shell.

## 2. Create a S3 bucket 

Amazon S3 is a Simple Storage Service, It allows people to store objects(files) in buckets...
Meanwhile, Buckets must have a globally unique name, defined at the region level and Objects(files) have a KEY

I created the s3 bucket using the command line below.

    aws s3 mb s3:// my-bucket-name --region us-east-1
   
   
## 3. Create a folder in your S3 bucket.

Amazon S3 is not a file system, it is an object storage. So in S3, there is no technical concept of a folder. Folders in S3 are meant only for organization purposes. For us to organize the objects that make sense for us. The Amazon S3 implements folder object creation by creating a zero-byte object.

So i created a new folder named new-folder and upload a file into that folder with this command line

[cloudshell-user@ip-10-1-58-48~] aws s3 ls s3://vink
          
                                           PRE / 
                                           PRE test-folder/
                                           
 2022-10-24 12:43:00         3411 block_ -3863181236475038926
 
 The we copy the file we mention the destination as new-folder/test-file eventhough new-folder doesn't exist
 
 [cloudshell-user@ip-10-1-58-48~] aws s3 cp s3://vink/new-folder/test-file
 
 we can now see the new-folder when we do a listing on the bucket.
 
  [cloudshell-user@ip-10-1-58-48~] aws s3 cp s3://vink
                                             PRE / 
                                             PRE new-folder/
                                             PRE test-folder/                   
 2022-10-24 12:43:00                        3411 block_ -3863181236475038926 
 
 
 which will also be seen on the AWS S3 console also.
 
 
 ## 4.  Upload objects to your S3 bucket
 I discovered that when you upload files to S3, you can upload one file at a time, or by uploading multiple files and folders recursively.Depending on your requirements, you may choose one over the other that you feel it appropriate.
 The command line i ran ti upload a file to S3 (you'll need to provide two arguments i.e. source and destination to the command)
 
     aws s3 cp c:\User\new-folder s://Styrene
     
 so i ran this command to check if it was uploaded
    
     aws s3 ls s3://Styrene
     
## 5.  List the object in your S3 bucket

To list all of the files of an S3 bucket with the AWS CLI, use this command line 

       aws s3 ls s3://YOUR_BUCKET
       
## 6. Download Object from your S3 bucket
There are varieties of ways to download files from an S3 Bucket, but if you are downloading an entire S3 Bucket then it is preferrably recommended using AWS CLI by running this command

              aws s3 sync s3://SOURCE_BUCKET LOCAL_DESTINATION
              
(i) To Download S3 Bucket to Current Local Folder
              
 To Download the whole S3 Bucket in the same folder that you are in, then i used the command       aws s3 sync s3://styrene .
 
 note: The Local_Destination is set to a dot ( . ). which means that you are downloading to the current folder that you are in .
 
(ii) To Download S3 Bucket to Different Local Folder

If you want to download the S3 Bucket to a different folder using AWS CLI, then you can point the LOCAL_DESTINATION to that folder.

I found that there are 2 ways to do this - via absolute path and relative path.

An absolute path is where you specified the exact path from the root volume where the destination folder is to achieve this i ran this code  

  aws s3 sync s3://Styrene C:\Users\user\cli-demo
  
 A relative path is where you specify the path to the target folder from the current folder that you are in... with this command line 
 
  aws s3 sync s3://vink . \Desktop\s3_download\
  
## 7. Delete object in your s3 bucket
To delete objects in an S3 bucket, the S3 bucket is empty.
   
        aws s3 rm s3://my-bucket
  
## 8. Delete your S3 bucket
Once all the objects have been deleted and the S3 bucket is empty, then it's possible to delete the S3 bucket using the command 

      aws s3 rb s3://my-bucket

