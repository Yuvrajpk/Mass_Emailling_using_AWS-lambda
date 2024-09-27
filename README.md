# Mass_Emailling_using_AWS-lambda
Mass emailing with AWS Lambda and Amazon SES allows you to send emails at scale efficiently. Lambda triggers, such as S3 file uploads or CloudWatch schedules, execute functions that send emails via SES. It's a cost-effective, serverless solution, ideal for large-scale email campaigns where you pay only for the resources and time used.

This project demonstrates how to set up a serverless solution for sending mass emails using AWS Lambda and Amazon Simple Email Service (SES). This setup is designed for high scalability, cost-efficiency, and ease of use.

# Features
Serverless: Powered by AWS Lambda, making it highly scalable and eliminating the need for managing servers.
Amazon SES Integration: Uses Amazon SES for reliable and secure email delivery.
Automated Trigger: Can be triggered via S3 upload, API Gateway, or CloudWatch scheduled events.
Customizable Email Templates: Supports dynamic email templates for personalization.
Batch Processing: Sends emails in batches to comply with SES sending limits.

# Architecture Overview
AWS Lambda: Executes the email sending logic.
Amazon SES: Sends the actual email messages.
Amazon S3: (Optional) Stores the recipient list files that trigger the Lambda function.
Amazon CloudWatch: (Optional) Can be used to trigger Lambda on a schedule.
Amazon API Gateway: (Optional) Allows HTTP API calls to invoke the Lambda function.

# Prerequisites
AWS Account with IAM permissions to create Lambda functions, S3 buckets, and access SES.
Node.js Installed (or the appropriate language environment, e.g., Python).
Amazon SES verified domain or email address for sending emails.
AWS CLI configured for deployment.

# Steps to be Followed
<b>Step 1:</b> Create an S3 Bucket -> Amazon S3 will store the CSV files containing the email addresses of the recipients. -> Navigate to S3: In the AWS Management Console, click on “S3” under the Storage category. -> Create a Bucket: Click on “Create bucket”. Name your bucket (it must be unique across AWS), select a region close to you for better performance, and then create the bucket.

<b>Step 2:</b> Set Up AWS Simple Email Service (SES) AWS SES will handle the email sending operations. -> Navigate to SES -> Verify Your Email Address: Before sending emails, SES requires verification of your ownership of the email address. On the left pane, go to Identities, and then verify the email address you want to send from. -> Important Note: As we are using SES in sandbox mode, you must manually verify each email address that you wish to send emails to before they can receive emails from your application. This is a restriction in the sandbox environment intended to prevent spam and abuse. -> Add and verify all Recipient Email Addresses: You can use Temp Mail for testing.

<b>Step 3:</b> Create an IAM Role for Lambda -> This role will allow your Lambda function to access AWS resources securely. -> Navigate to IAM: Go to “IAM” under Security, Identity, & Compliance. -> Create a New Role: Click on “Roles”, then “Create role”. Choose “Lambda” for the service that will use this role, then proceed to permissions. -> Attach Policies: Add policies like AmazonSESFullAccess, AmazonS3FullAccess, and AWSLambdaExecute.

<b>Step 4:</b> Create a Lambda Function -> This function will process the CSV file and send emails. -> Navigate to Lambda: Go to “Lambda” under Compute. -> Create Function: Choose “Author from scratch”, name your function, select Python 3.x for the runtime. -> Set Permissions: Choose the IAM role you created earlier. -> Create Function: Finalize the creation of your function.

<b>Step 5:</b> Write Lambda Function Code -> The function will read from S3, parse CSV, and send emails via SES.

<b>Step 6:</b> Set Up S3 Event Trigger -> Trigger your Lambda function when a CSV file is uploaded to S3. -> Select Your Function: In Lambda, open your function’s configuration. -> Add Trigger: Choose “S3” from the list. Configure the trigger for “PUT” events, and set the file prefix or suffix (like .csv). -> Save: Save your configuration.

<b>Step 7:</b> Test Your Setup -> Upload a CSV file with an ‘email’ column to your S3 bucket and check the Lambda execution logs. Make sure the emails are being sent out successfully.

# Usage
Upload a file (CSV/JSON) with recipient emails to the configured S3 bucket.
Trigger Lambda via API Gateway or CloudWatch events to start sending emails.
Monitor email sending status and metrics via CloudWatch logs and SES dashboards.

# Limitations
SES has sending limits based on your account tier. Make sure to monitor your sending limits in the SES console.
Lambda has a 15-minute timeout limit, so for large email lists, batching is recommended.

# Monitoring & Logs
CloudWatch Logs: Track Lambda execution logs.
SES Metrics: Use the SES dashboard to monitor email bounce rates, complaints, and delivery metrics.

# Conclusion
Successfully built a basic mass emailing system using AWS. This system is not only scalable but also cost-effective, perfect for businesses looking to manage their email marketing efforts. Always ensure to comply with legal requirements and manage opt-ins and opt-outs to respect user privacy and avoid spam.

# License
This project is licensed under the MIT License - see the LICENSE file for details.
