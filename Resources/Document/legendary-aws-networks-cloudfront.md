# Website Delivery with CloudFront

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-cloudfront)

**Author:** Manish Sharma  
**Email:** manishsharma7@hotmail.com

---

## Website Delivery with CloudFront

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-cloudfront_1dddddwe)

---

## Introducing Today's Project!

In this project, we will demonstrate how to create and host a static website using AWS services, with the goal of learning more about cloud-based web hosting. We will begin by creating a storage space in Amazon S3 to store our website’s files. Next, we will set up Amazon CloudFront to distribute the website content globally, ensuring low latency and high availability for users around the world. As part of the process, we will manage permissions for both S3 and CloudFront to maintain secure access to our resources. Finally, we will compare different methods for hosting websites on AWS and analyze their performance in terms of speed, reliability, and scalability.

### Tools and concepts

Services we used include CloudFront and S3
Key concepts we learnt include content delivery network (CDN), distributions, origin access control (OAC), performance load time. S3 static website hosting vs CloudFront.

### Project reflection

This project took me approximately 1 hour. The most challenging part was understanding Origin Access Control (OAC)—how it works and why it's needed to securely connect CloudFront to a private S3 bucket. The most rewarding part was comparing performance load times and seeing CloudFront outperform S3, which clearly demonstrated the benefits of using a content delivery network for faster, global content delivery.

We did this project today to learn about CloudFront and content delivery. This project met our goals, and we’ve successfully built the presentation tier of a three-tier architecture. By setting up S3, configuring CloudFront with Origin Access Control, and comparing performance and security, we gained hands-on experience with delivering static content efficiently and securely.

---

## Set Up S3 and Website Files

I started the project by creating an S3 bucket to store my content. I can't use CloudFront for this task because CloudFront is not a storage service; it's a content delivery network (CDN) that distributes content globally for low latency and high transfer speeds. The S3 bucket acts as the origin, holding my website’s static files like HTML, CSS, and images, which CloudFront can then cache and deliver efficiently to users around the world.

The three files that make up my website are index.html, which defines the structure (text and images) and content of the web page; style.css, which contains the styles and layout rules that make the website visually appealing; and script.js, which adds interactivity and dynamic behavior to the site.

We validated that our website files work by opening index.html locally in our browser. We saw a simple webpage without any errors, confirming that all components—HTML, CSS, and JavaScript—are functioning correctly. This means the three files are ready to be uploaded to the S3 bucket for hosting and distribution.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-cloudfront_qgo7wcd3)

---

## Exploring Amazon CloudFront

Amazon CloudFront is a content delivery network, which means it caches web content (i.e. website files) to edge location around the world. Business and developers use CloudFront because it speeds up their website perfomance. 

To use Amazon CloudFront, we set up distributions, which are instructions that tell CloudFront how to deliver your content. We set up a distribution for our website and the origin is S3 Bucket

Our CloudFront distribution's default root object is index.html This means that when user visit our websit's root URL, they will see the content described in index.html

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-cloudfront_qgo7wcdt)

---

## Handling Access Issues

When I tried visiting my distributed website, I ran into an access denied error because origin access settings were Public, even though the origin was publicly accessible, the individual objects in the S3 bucket were still private by default.

My distribution's origin access settings were Public. This caused the access denied error because, even though the origin was publicly accessible, the individual objects in the S3 bucket were still private by default. Without updating the object permissions to allow public read access, CloudFront couldn’t retrieve and serve the content, resulting in an access denied error.

To resolve the error, we set the origin access control (OAC). OAC is a special user that's created to connect S3 with CloudFront (i.e give CloudFront access) while still keeping out public access to the bucket's object. This improves security for our content. 

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-cloudfront_egrhntyu)

---

## Updating S3 Permissions

Once I set up my OAC, I still needed to update my bucket policy because the S3 bucket must explicitly grant permission to the CloudFront service using the OAC’s identity. While OAC establishes a secure connection between CloudFront and the bucket, the bucket policy controls who can access the objects.

Creating an OAC automatically gives me a policy I could copy, which grants CloudFront permission to access objects in my S3 bucket using the OAC's service principal. This policy ensures that only CloudFront, and not the general public, can retrieve the files from the bucket, maintaining security while allowing global distribution of my website content.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-cloudfront_eg98ntyu)

---

## S3 vs CloudFront for Hosting

For my project extension, I'm comparing S3 with CloudFront. We initially had an error with static website hosting because of access issues. This time, the error occurred because we enabled S3 static website hosting without making our objects publicly available. Even though the website hosting feature was turned on, S3 objects remain private by default, so users couldn’t access the content until we explicitly updated the object permissions to allow public read access.

We tried resolving this by turning off Block Public Access settings. However, we still ran into a 403 Forbidden error when accessing the static website URL, because the bucket policy still didn’t allow public access to the objects. Disabling Block Public Access only makes it possible to apply public permissions, but until the bucket policy is explicitly updated to grant public read access, users will continue to be denied access to the website content.

We could finally see our S3 hosted static website when we updated our bucket policy to allow the public to access the bucket's object. This worked because our bucket policy previously only allowed CloudFront access, so changing S3 permission is required.

ompared to the permission settings for our CloudFront distribution, using S3 meant we had to enable public access to our bucket. We preferred using CloudFront because it allows us to keep the bucket private and restrict access to CloudFront only through Origin Access Control (OAC). This setup is more secure, as it prevents direct public access to the S3 bucket while still enabling global content delivery through CloudFront.

---

## S3 vs CloudFront Load Times

Load time means the amount of time it takes for a website to fully display its content in a user's browser. The load times for the CloudFront site were faster than the S3 site because CloudFront is a content delivery network (CDN) that caches content at edge locations around the world. This means users can access the website from a server closer to their physical location, reducing latency and improving performance. In contrast, S3 serves content from a single AWS region, which can result in slower load times for users who are farther away from that region.

A business would prefer CloudFront when performance, scalability, and security are critical—especially for websites with a global audience.
S3 static website hosting might be sufficient when the website is simple, serves a local or limited audience, and doesn't require low latency or advanced security. It's easier to set up and cost-effective for basic, low-traffic use cases.

![Image](http://learn.nextwork.org/elated_cyan_peaceful_duck/uploads/aws-networks-cloudfront_12verpuh)

---

---
