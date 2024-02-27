# Holiday Rental Property Management Tool

For this project I imagined to host the client side application in an S3 bucket backed by a Cloudfront distribution to enforce HTTPS, global distribution and reduced latency. The client side application will have two main users: guests and hosts. Hosts can login using AWS Cognito, Guests can only see the property and book a room.

The Host flow is the following:

- Host signs up for the platform and chooses his own subdomain
- if available, a new record is created on S3 and a dedicated user pool in AWS Cognito
- they connect their Stripe account

The main CRUD operations are implemented through an API Gateway with a specific Lambda function for each operation. The Lambda functions stores record in a DynamoDB Table. The DynamoDB table has Dynamo Streams configured so everytime there is a new reservation, an update on an existing reservation or a cancelled reservation, the update is reflected into DynamoDB Streams and can be streamed to 3rd party platform to keep the calendar synched. The same behaviour, on the other way around, so when people book from 3rd party platform, triggers a webhook which is a Lambda function behind the same API gateway, which creates a record in DynamoDB.

All the notifications through emails are handled by AWS SES, which will be called from Lambda functions when needed (new reservations, cleaners, doors key).

Each of the automated tasks such as check in in 10 days, cleaners notifications, checkout schedulers, door keys are handled with an Amazon Eventbridge Scheduler which runs daily and query the dynamoDB table (by PK to keep it efficient) to retrieve reservations and send notifications accordingly. There will be a scheduler per each notification

Example

Type of reminder: check in arrival in one day. Scheduler runs every day and query reservations for that specific day + 1. In this way we know get tomorrow's arrivals and we send the door's key email.

If you want to follow the architecture explanation on video, please join me here: https://www.youtube.com/watch?v=mRrYAL6FAJ0
