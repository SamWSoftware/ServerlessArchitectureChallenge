# Holiday Rental Management

This pattern demonstrates how to automate the setup and deployment of a sample application (which handles holiday rental management) with serverless technologies such as AWS Lambda, Amazon API Gateway and Amazon DynamoDB.

1. The user's DNS request are served by Amazon Route 53, a highly available Domain Name System Service (DNS). Network traffic is routed to infrastructure running in Amazon Web Services.

2. Static content is delivered by Amazon CloudFront, a global network of edge locations. Requests are automatially routed to the nearest edge location. The static resources and content are stored in
   Amazon Storage Service (S3), a highly durable storage infrastructure designed for mission-critical and primary data storage. S3 servres the static content for the website such as HTML,
   CSS and Javascript files.

3. A user firsts authenticates using (Amazon Cognito User Pools), the client calls out to Amazon Cognito in order to obtain temporary credentials.

4. API requests are signed using the temporary credentials obtained from Amazon Cognito and sent to the Amazon API Gateway service which provides features such as security and throttling
   for your APIs. Requests are passed through the API Gateway where they can be transformed and passed through to the backend service logic.

5. AWS Lambda provides the backend business logic for your web application. You do not run servers, but instead upload code to AWS which will be invoked when request comes into your API.
   The service is highly scalable and removed the need to manage is infrastructure.

6. As a fully managed database solution, Amazon Dynamo DB provides fast, consistent, performance as the data layer for your web application.

7. Stripe offers both the ability to make instant payments for direct bookings. When a purchase is successfully completed, Stripe will notify you using a web hook that you define. 

8. Dynamo DB Stream has been configured for syncing booking creation, deletion and updation details to the third party rental platforms using Lambda. Similarly, when visitor book through one of the tird party platform, it will be updated in Dynamo DB using webhook url.

9. Eventbridge scheduler has been configured for completing scheduling tasks (for booking cleaners, remainder email before 10 days of reservation, accessing and chaging the access code key.

10. All emails will be triggered using Amazon SES.
