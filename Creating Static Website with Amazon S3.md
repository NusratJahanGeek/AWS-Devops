# Lab - 2
## Creating Static Website with Amazon S3

In this lab, I will learn the process of creating a static website by using Amazon Simple Storage Service (Amazon S3), how to configure an S3 bucket policy, which is required to allow public access.
By the end of this lab, I will have hands-on experience with the AWS Management Console and develop a better understanding of the AWS Cloud overall.

## Objective - 1: Create an S3 bucket

The bucket name must be unique within a partition. A partition is a grouping of Regions. 
AWS currently has three partitions: aws (Standard Regions), aws-cn (China Regions), and aws-us-gov (AWS GovCloud (US) Regions).

![image](https://github.com/user-attachments/assets/a7fd2afa-cb2c-43c8-8062-5da13ca57d1f)

By default, Amazon S3 now applies server-side encryption with Amazon S3 managed keys (SSE-S3) as the base level of encryption for every bucket in Amazon S3. With this encryption, all new object uploads to Amazon S3 are automatically encrypted at no additional cost and with virtually no impact on performance. Additionally, the buckets block public access unless we specifically choose to make them publicly available.

## Objective - 2: Configure the S3 bucket as a static website and allow public access.

### Step - 1: Configure the S3 bucket as a static website

![image](https://github.com/user-attachments/assets/a7761393-ab9c-4451-a9ba-1d66956251d1)

### Step - 2: Allow public access to the bucket
By default, Amazon S3 blocks public access to our account and buckets. If we want to use a bucket to host a static website, we must allow public access to the bucket.

![image](https://github.com/user-attachments/assets/50ab4ba2-8c44-40b2-a949-2100f4bf3b5e)


## Objective - 3: Add a bucket policy to allow public access to content in the bucket

Now I need to add a bucket policy to grant public read access to content in my bucket. When I grant public read access, anyone on the internet can access my bucket. I can accomplish this task by adding the s3:GetObject action to my S3 bucket and setting the Principal value to *, which represents anyone.

![image](https://github.com/user-attachments/assets/02ac11af-63dd-41f4-9223-5c53204da792)

In this policy, I am granting GetObject permissions for my specific bucket to anyone.


## Objective - 4: Create and upload the website assets and test the website

In this task, I will create and upload the website assets to my S3 bucket. Website assets include images, style sheets, scripts, fonts, and other files that contribute to the visual and functional aspects of the website.

### Step - 1: Create the website assets
I've created an index.html and error.html for this task.

![image](https://github.com/user-attachments/assets/a0f18f27-fb22-4a00-b70d-42e34f078634)

### Step - 2: Upload the website assets to your bucket

![image](https://github.com/user-attachments/assets/6cfec417-dada-4b57-9e74-9717ddb53446)

## Objective - 5: Test the Amazon S3 static website.
Voila! Now my website is live with the URL.

![image](https://github.com/user-attachments/assets/d2156317-7a9e-47b6-ab0a-d4a00c0ad104)

The error page is also showing up perfectly. Here, the browser can’t find the path to the /aboutus location, so the error.html page is returned as expected.

![image](https://github.com/user-attachments/assets/a65a9c0b-e3a6-448b-b799-1e6834c378ea)

