# Lab - 2: Creating a Static Website with Amazon S3

In this lab, I’ll walk you through the steps I took to create a static website using Amazon Simple Storage Service (Amazon S3). I’ll also explain how to configure an S3 bucket policy for public access. By the end, I’ll have hands-on experience with the AWS Management Console and a stronger understanding of the AWS Cloud.

## Objective 1: Create an S3 Bucket

The first step in creating a static website is setting up an S3 bucket. In Amazon S3, bucket names must be unique within a partition (a grouping of AWS regions). AWS currently has three partitions: `aws` (Standard Regions), `aws-cn` (China Regions), and `aws-us-gov` (AWS GovCloud).

![S3 Bucket Creation](https://github.com/user-attachments/assets/a7fd2afa-cb2c-43c8-8062-5da13ca57d1f)

By default, Amazon S3 now applies server-side encryption (SSE-S3) to all new object uploads, keeping data secure without any extra cost or impact on performance. The buckets also block public access by default unless I explicitly make them public.

## Objective 2: Configure the S3 Bucket as a Static Website

### Step 1: Set Up Static Website Hosting

To enable website hosting, I configured my bucket to host static content.

![Static Website Configuration](https://github.com/user-attachments/assets/a7761393-ab9c-4451-a9ba-1d66956251d1)

### Step 2: Enable Public Access

Since Amazon S3 blocks public access by default, I needed to allow public access for my bucket to act as a static website.

![Public Access Settings](https://github.com/user-attachments/assets/50ab4ba2-8c44-40b2-a949-2100f4bf3b5e)

## Objective 3: Add a Bucket Policy for Public Access

To grant public read access to my website content, I added a bucket policy. I used the `s3:GetObject` action and set the `Principal` value to `*`, allowing anyone to read the objects in my bucket.

![Bucket Policy](https://github.com/user-attachments/assets/02ac11af-63dd-41f4-9223-5c53204da792)

This policy provides `GetObject` permissions to anyone for the specified bucket.

## Objective 4: Create and Upload Website Assets

In this step, I created and uploaded the website assets, such as `index.html` and `error.html`, to my S3 bucket. These assets include files that contribute to the site’s look and functionality, like images, stylesheets, and scripts.

### Step 1: Create Website Files

I created the main files, including `index.html` and `error.html`, to serve as the website’s core pages.

![Website Files](https://github.com/user-attachments/assets/a0f18f27-fb22-4a00-b70d-42e34f078634)

### Step 2: Upload Website Files

Then, I uploaded these files to my bucket.

![Upload Files](https://github.com/user-attachments/assets/6cfec417-dada-4b57-9e74-9717ddb53446)

## Objective 5: Test the Amazon S3 Static Website

With everything in place, my website is now live and accessible via the generated URL!

![Website URL](https://github.com/user-attachments/assets/d2156317-7a9e-47b6-ab0a-d4a00c0ad104)

The error page is also functioning correctly. If someone tries to visit a nonexistent path, like `/aboutus`, they’ll automatically be redirected to `error.html`.

![Error Page](https://github.com/user-attachments/assets/a65a9c0b-e3a6-448b-b799-1e6834c378ea)
