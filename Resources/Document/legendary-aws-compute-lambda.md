<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Fetch Data with AWS Lambda

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-lambda)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Fetch Data with AWS Lambda

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-lambda_p9thryj2)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use AWS Lambda to retrieve data that's in a DynamoDB database. I'm doing this project to learn how to set up the data tier of a web app and connect that with a Lambda function too (logic tier).

### Tools and concepts

The services I used in this project were Amazon DynamoDB and AWS Lambda. Key concepts I learned include how Lambda functions work, adding items to DynamoDB tables, testing Lambda functions, selecting the right permission policies, and writing custom inline policies.

### Project reflection

This project took me approximately 1 hour and 15 minutes, including demo time. The most challenging part was writing my own inline policy — a totally new experience. The most rewarding moment was seeing the correct data appear when I ran a successful function test.

I did this project today to learn about the data tier in a three-tier architecture. It definitely met my goals, as I also learned how to connect it to AWS Lambda, which serves as the logic tier.

---

## Project Setup

To set up my project, I created a database using DynamoDB.
DynamoDB is a NoSQL database, so it is very fast at retrieval and flexible for data storage. The partition key is userld, which means the key identified for each data is its userld.

In my DynamoDB table, I added a piece of data.
DynamoDB is schemaless, which means that the data we add can come with new attributes, and ever piece of data can have its set of attributes without affecting other data.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-lambda_a112c3d5)

### AWS Lambda

AWS Lambda is a service that lets us run code without having to manage servers. We're using Lambda in this project to create a function (i.e. a piece of code) that retrieves data from a DynamoDB table.

---

## AWS Lambda Function

My Lambda function has an execution role, which is the set of permissions that it has to interact with other AWS services. By  default, the role grants basic Lambda permissions, which are the pemissions to write logs with CloudWatch e.g. error logs.

My Lambda function is designed to retrieve data from a DynamoDB table. The first half of the code focuses on fetching the data from the database. The second half handles sending the appropriate responses—such as success messages, “item not found” notifications, or error messages—back to the requester.

The code uses the AWS SDK, which is a set of tools that makes it easier for developers to interact with AWS services in their application code. In our case, the SDK is used to perform DynamoDB actions, such as reading and retrieving data items.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-lambda_a1b2c3d5)

---

## Function Testing

To test whether my Lambda function works, I wrote a test event in the Test tab of the Lambda console. The test is written in JSON. If it’s successful, I should see the correct piece of data in JSON when I query for userId = 1.

The test showed a “success” because the function ran without any errors — meaning there were no syntax or dependency issues. However, the actual response from the function was an error, because my Lambda function was trying to retrieve data from DynamoDB without the necessary permissions.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-lambda_u1v2w3x4)

---

## Function Permissions

To resolve the AccessDenied error, I gave my Lambda function permission to perform the GetItem action on the DynamoDB table. This is because GetItem is the action my Lambda function was blocked from performing.

There were four DynamoDB permission policies I could choose from, but I didn’t pick AWSLambdaDynamoDBExecutionRole or AWSLambdaInvocation-DynamoDB because they relate to DynamoDB Streams — live updates of table items that have changed.

I also didn’t choose AmazonDynamoDBFullAccess because it would give my Lambda function permission to do far more than necessary with the table. ReadOnlyAccess was the right choice, as it limits the function to just reading data and helps protect the table from unauthorized access through Lambda.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-lambda_3ethryj2)

---

## Final Testing and Reflection

To validate the new permission settings, I re-tested my Lambda function. The result was a piece of data with three attributes — email, name, and userId — exactly matching the data I input into the database at the start of this project!

Web apps are a popular use case for using Lambda and DynamoDB. For example, I could use Lambda to retrieve product information, user profiles, or content (like blogs or news articles) based on user queries or actions within my web app.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-lambda_p9thryj2)

---

## Enahancing Security

For our extension, I challenged myself to replace the permission policy I previously granted to my Lambda function. Instead of using the AWS-managed policy, I’ll ensure it can only access the UserData table. This will enhance the security of our DynamoDB database.

<nil>

When updating my Lambda function’s permission policies, there’s a risk of accidentally removing access to resources or actions it needs to work. To be sure, I re-tested the function after updating its permissions — and it still works perfectly.

---

---
