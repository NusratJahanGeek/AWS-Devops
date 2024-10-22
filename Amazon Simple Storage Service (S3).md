# Lab - 1
## Introduction to Amazon Simple Storage Service (S3)

Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means customers of all sizes and industries can use it to store and protect any amount of data for a range of use cases, such as websites, mobile applications, backup and restore, archive, enterprise applications, Internet of Things (IoT) devices, and big data analytics. Amazon S3 provides easy-to-use management features so you can organize your data and configure finely-tuned access controls to meet your specific business, organizational, and compliance requirements. Amazon S3 is designed for 99.999999999% (11 9’s) of durability and stores data for millions of applications for companies all around the world.

## Lab Scenario

Assuming I work for a company using Amazon S3 for data storage. An application residing on an EC2 instance needs to push reporting data to an S3 bucket daily. I am tasked with creating an S3 bucket for my company to use for storing this report data. For a successful deployment, I need to ensure the EC2 instance has enough privileges to upload and retrieve data from the S3 bucket. For security reasons, only the EC2 instance can write data to the S3 bucket. The files in the S3 bucket also require protection against accidental deletion.

## Objective - 1: Create a Bucket in Amazon S3

I am new to Amazon S3 and want to test its features and security as I configure the environment to hold the EC2 report data. Since every object in Amazon S3 is stored in a bucket, creating a new bucket to hold the reports is the first task on my list.

In this task, I'll create a bucket to hold my EC2 report data and then examine the different bucket configuration options.

![Create Bucket](https://github.com/user-attachments/assets/24a77311-cc1d-4dfb-bf48-11fffbe7893f)

## Objective - 2: Upload an Object to the Bucket

An object can be any kind of file: a text file, a photo, a video, a zip file, and so on. When I add an object to Amazon S3, I have the option to include metadata with the object and set permissions to control access.

![Upload Object](https://github.com/user-attachments/assets/e88626ef-55c5-4de8-8963-84ba43785094)

## Objective - 3: Manage Access Permissions on an Object and a Bucket

Security is a priority in Amazon S3. Before I configure my EC2 instance to connect to the report bucket, I want to test the bucket and object settings for security.

The uploaded file showed an 'access denied' error. This is because objects in Amazon S3 are private by default.

![Access Denied](https://github.com/user-attachments/assets/cd1af3e6-2733-4e62-b579-8f0745b3909c)

### Steps Taken:
1. **First, I updated the "Block Public Access" settings:**

   ![Block Public Access](https://github.com/user-attachments/assets/f86d8f88-dfbe-41a3-a412-1ec8da4a73aa)

2. **Then, I made the object publicly accessible by clicking on "Make public via ACL":**

   ![Make Public via ACL](https://github.com/user-attachments/assets/13ea9234-c62a-42b4-9846-0e414f8dbcec)

   Hence, the object became visible with the URL.

   ![Object Visible](https://github.com/user-attachments/assets/fd5f8e74-bc5e-4ac7-bf5a-6477440bf761)

In this case, I granted read access to just one specific object. If I wish to grant access to the entire bucket, I will need to use a bucket policy, which I will configure later.

## Objective - 4: Test Connectivity from the EC2 Instance

Now, I will connect to my Amazon Elastic Compute Cloud (Amazon EC2) instance to test connectivity and security with the S3 report bucket.

Session Manager enables us to connect to the bastion host instance without the need for specific ports to be open on the firewall or Amazon Virtual Private Cloud (Amazon VPC) security group.

![Session Manager](https://github.com/user-attachments/assets/cc66dc8a-8ef2-42a1-acdb-c6e1da8184d4)

Here, the output indicates an error: *upload failed*. This is because we have read-only rights to the bucket and do not have permission to perform the `PutObject` operation. I will create a bucket policy to grant `PutObject` permissions.

## Objective - 5: Create a Bucket Policy

A bucket policy is a set of permissions associated with an S3 bucket. It is used to control access to an entire bucket or specific directories within a bucket.

## Objective - 6: Use Bucket Versioning

Versioning in Amazon S3 allows us to preserve, retrieve, and restore every version of every object stored in an S3 bucket. I will enable versioning on the bucket to protect against accidental deletions or overwrites.
