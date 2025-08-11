# Build a Three-Tier Web App

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-threetier)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Build a Three-Tier Web App

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_2b3c4d5e)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up a three-tier web app from scratch! I’ll start with the presentation tier, then set up the logic tier, and finally configure the data tier before tying them all together.

### Tools and concepts

The services I used were Amazon S3, CloudFront, DynamoDB, Lambda, and API Gateway. Key concepts I learned include how Lambda functions work, handling CORS errors, updating the JavaScript file with the API Invoke URL, and testing the API Invoke URL directly in the browser.

### Project reflection

This project took me approximately 5 hours. The most challenging part was resolving the CORS errors in both API Gateway and Lambda and troubleshooting along the way. The most rewarding moment was seeing the final outcome—user data successfully returned in my web app.

I did this project today to learn about three-tier architecture and set up my own web app. This project definitely met my goals, and I was able to see a fully functioning web app by the end.

---

## Presentation tier

For the presentation tier, I will set up how my website is displayed and made available to end users. This is because the presentation tier is responsible for storing my website’s files using Amazon S3 and distributing them via Amazon CloudFront.

I accessed my deployed website by visiting the CloudFront distribution’s URL. This URL works because I set up an origin access control that restricts my S3 bucket’s access to only the CloudFront distribution.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_3a4b5c6d)

---

## Logic tier

For the logic tier, I will set up a Lambda function to handle requests (e.g., looking up a userId to return user data) and create an API using API Gateway to receive requests from users and forward them to the Lambda function.

My Lambda function retrieves data by looking up a userId (which the user enters through the web app) in DynamoDB. The AWS SDK is used in the function code, so I can use templates and libraries that help me find the correct DynamoDB table and request data.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_6a7b8c9d)

---

## Data tier

For the data tier, I will set up a DynamoDB database to store user data. At the moment, there is no user data for me to return to the web app’s users. The data in my database will be returned once I set up DynamoDB and connect it with Lambda.

The partition key for my DynamoDB table is userId. This means when the table looks up user data, it does so based on userId. Then, it returns all data (values) related to the item with that ID.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_u1v2w3x4)

---

## Logic and Data tier

Once all three layers of my three-tier architecture are set up, the next step is to connect the presentation and logic tiers. That’s because, currently, there’s no way for my API to receive requests that users make through the distributed site.

To test my API, I visited the Invoke URL of the production stage API. Initially, I encountered an error, but I resolved it by enabling Lambda proxy integration under API > Resource > GET > Integration Request. This setting sends the request to my Lambda function as a structured event. After fixing this, I was able to retrieve user data in JSON when I looked up userId=1, confirming the connection between the logic and data tiers.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_a112c3d5)

---

## Console Errors

The error on my distributed site was caused by a problem in script.js — one of the website files I uploaded to S3. The script.js file was referencing a production API endpoint incorrectly, which caused the issue.

To resolve the error, I updated script.js by replacing placeholder text with the API’s production stage Invoke URL. Then, I re-uploaded script.js to S3 because the bucket was still serving the previous version that contained the error.

After updating script.js, I ran into a second error — a browser-side CORS issue. This happened because API Gateway, by default, only allows requests from users directly accessing its Invoke URL in the browser, not from CloudFront.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_a1b2c3d5)

---

## Resolving CORS Errors

To resolve the CORS error, I first went into my API in API Gateway and enabled CORS on the /users resource. Then, I ensured GET requests were allowed and added my CloudFront domain to the list of allowed origins.

I also updated my Lambda function code to include the necessary CORS headers so it can properly respond to API requests. Specifically, I added the 'Access-Control-Allow-Origin' header in the function’s response to indicate that it allows requests from the API’s URL.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_1qthryj2)

---

## Fixed Solution

I verified the fixed connection between API Gateway and CloudFront by looking up user data on the distributed site again. In this final test, the user data was successfully returned—confirming that a user request from the presentation tier retrieves data from the data tier.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-compute-threetier_2b3c4d5e)

---

---
