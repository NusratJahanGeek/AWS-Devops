# Lab - 3: Hosting WordPress Using Amazon S3

In this lab, I’ll convert a WordPress site from Amazon EC2 into a static website hosted on Amazon S3. WordPress is a popular, open-source CMS that powers over 60 million sites and is easily extended with plugins and templates. While WordPress sites are dynamic (requiring server-side processing), converting to static hosting on S3 minimizes maintenance, reduces hosting costs, and increases scalability by removing the need for server-side scripts.

![Overview](https://us-west-2-tcprod.s3.us-west-2.amazonaws.com/courses/spl-39/v4.1.14.prod-c48d9fd0/scripts/overview.jpg)

## Objective 1: Configure WordPress on an Amazon EC2 Instance

To start, I created a WordPress website on an EC2 instance and added a sample blog post.

![WordPress Dashboard](https://github.com/user-attachments/assets/2ab554a0-324e-4d06-9d83-467ab1363a4e)
![Sample Blog Post](https://github.com/user-attachments/assets/5a0102fd-89fc-4345-b669-08d865e39b27)

## Objective 2: Create an S3 Bucket with Static Website Hosting

Next, I created an Amazon S3 bucket configured for static website hosting. I enabled "ACLs enabled," "Object Writer," and deselected "Block All Public Access." Then, I enabled the "Static Website Hosting" option.

![S3 Static Hosting](https://github.com/user-attachments/assets/b898aa83-10b5-4b38-87f8-f4faeceda275)

## Objective 3: Generate a Static Version of WordPress

I used the `wp-static` utility to generate HTML copies of my WordPress website, converting it into static files that don’t require WordPress to serve content.

![Static Conversion](https://github.com/user-attachments/assets/4efc480f-eb46-41d6-a91f-cf1779fc765c)

## Objective 4: Upload Static Pages to Amazon S3

I used the AWS CLI to copy these static pages to my S3 bucket, allowing the site to be accessible even if my WordPress server is turned off. Hosting on Amazon S3 offers high scalability and reduces EC2 costs, as no instances need to be running.

![AWS CLI Copy](https://github.com/user-attachments/assets/85a6fd67-f3bd-40c8-9ec3-a77e27eadc4a)

## Objective 5: Automate Uploads with a Script

To streamline updates, I created a shell script that extracts updated static files from WordPress and uploads them to Amazon S3. Now, when I make changes to my WordPress site, I only need to run the script to sync the latest content.

```bash
# Change to the WordPress directory
cd /var/www/html/wordpress

# Delete the old static files
sudo rm -rf wordpress-static

# Generate new static files
sudo /bin/sh wpstatic.sh -a

# Upload files to S3
aws s3 sync --acl public-read --delete /var/www/html/wordpress/wordpress-static s3://$BUCKET
