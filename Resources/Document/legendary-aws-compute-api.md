<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# APIs with Lambda + API Gateway

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-api)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-api_c9d0e1f2)

---

## Introducing Today's Project!

In this project, I'll demonstrate how to set up an API using AWS Lambda and Amazon API Gateway. I'm doing this project to learn how APIs work and to set up a snazzy logic tier in our three-tier architecture. By integrating Lambda with API Gateway, I'll create a serverless backend that can process requests, execute logic, and return responses—all without managing traditional servers.

### Tools and concepts

I used Amazon API Gateway and AWS Lambda in this project. I learned key concepts such as Lambda functions, API resources and methods, Lambda proxy integration, writing API documentation, managing API stages, and using the Invoke URL to access the API.

### Project reflection

This project took me approximately 1 hour to complete. The most challenging part was understanding and writing the Lambda function. The most rewarding part was creating the resources and methods—it was super informative and helped me better understand how APIs are structured.

I did this project to learn how to set up the logic tier of a web app—i.e., the 'backend' or the brains of the application. This project definitely met my goals, and I learned a lot about how an API works along the way.

---

## Lambda functions

AWS Lambda is a servie that lets us run code without having to manage any servers ourselves. That's why its is called a serverless server, or Function as a service (FaaS). I am using Lambda in this project to run code that helps me retrieve data.

The code I added to our function will grab a userID from a triggered event (i.e submitting a userID through a form/field in a website) and queries for a piece of data in DynamoDB that matches the userID. The code also takes of error handling

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-api_a1b2c3d5)

---

## API Gateway

APIs are tools that enable communication between systems. There are different types of API's like REST API,, HTTP APIs or WebSocket API. For this project I am using REST API,  it uses HTTP methods and is compatible with most programming languages + Lambda

Amazon API Gateway is a AWS service that helps developers with creating, maintaining and monitoring APIs. I am using API Gateway in this project to connect my web app users with my Lambda functions (i.e. the serverless backend)

When a user makes a request i.e. click on a "Get User Data" button. API Gateway's role is to receive the traffic determine whether or not it's authorized, and pass it through to Lambda if it is. API Gateway is also a traffic manager for requests.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-api_m3n4o5p6)

---

## API Resources and Methods

An API is made up of resources, which represent different sections or parts of the same API. For example, an API might have separate resources for retrieving user data, messaging data, and product data within the same application.

Each resource consists of methods, which are actions you can perform on that resource. API methods are based on standard HTTP methods—commands that allow you to interact with data over the internet. For example:

GET to retrieve data,
POST to add new data,
PUT to update existing data, and
DELETE to remove data.

I created a GET method that connects the API Gateway to our Lambda function. This means that when an end user sends a request to something like "api.com/users", the API knows to forward the request to our Lambda function—specifically when the user is trying to retrieve data.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-api_c9d0e1f2)

---

## API Deployment

When you deploy an API, you deploy it to a specific stage. A stage is like a snapshot of your API that helps you manage different versions or environments. We deployed to the production stage, also known as 'prod', which is where live traffic is directed and real users interact with the API.

To test my API, I visited the Invoke URL for the API deployed to the production stage. However, the API returned an error because the Lambda function it’s connected to doesn’t have the necessary permissions to access DynamoDB. Additionally, the DynamoDB table it’s supposed to interact with hasn’t been created yet, which can also cause authentication or access issues.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-api_3ethryj2)

---

## API Documentation

In this secret mission, I will write documentation for the API itself. This is because API documentation helps other developers understand the purpose, functionality, and use cases of my API.

Once I prepare my documentation, I can publish it to the production stage. Publishing to a specific stage is necessary because different stages represent different versions of the same API, so having tailored documentation for each stage is helpful.

My published and downloaded documentation showed me both our manually written work and some automatically generated documentation from API Gateway. We can upload this into tools like Swagger or Redoc to generate beautiful we pages about our API

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-api_z9a0b1c2)

---

---
