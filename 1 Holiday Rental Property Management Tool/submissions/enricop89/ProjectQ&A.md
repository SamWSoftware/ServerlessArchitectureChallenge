# AWS Well Architected

## Security

1. How do you secure your data in transit?

Data in transit is secured by applying HTTPS for each request.

2. How do you secure your data at rest?

Data at rest is secured using encryption at rest in S3 and databases (DynamoDB)

3. How is your architecture protected against malicious intent?

APIs: Access are controlled by JWT handled by AWS Cognito.

Storage: each function calling S3 and Database has only the necessary privilege, following the least privilege principal.

## Reliability:

1. How would your infra react if an availability zone went offline for an hour?

API: Lambda runs your function in multiple Availability Zones to ensure that it is available to process events in case of a service interruption in a single zone. Same for API Gateway

Storage: S3 is replicated into multiple AZs. DynamodB same, it is replicated in 3 AZs within the same region.

2.  Would your application still be usable?

Yes

3. Would there be any temporary or permanent loss of data? Would that be acceptable?

There shouldn't be any permanent loss of data, there might be some temporary 5xx errors. I believe, based on the nature of the application, that is acceptable.

5. How would your infra react if a whole region went offline for an hour? Would your application still be usable?Would there be any temporary or permanent loss of data? Would that be acceptable?

In the current design, the platform wouldn't be usable.

8. How would your application react if your traffic increased 10x in 5 minutes? (An advert plays on tv)

The application will scale automatically based on the traffic, there might some requests throttled but only temporary

9. Would your compute and database scale up to handle this quick increase in traffic
   Might you hit some service limits?

Yes, compute and database will scale and shouldn't hit any service limits

10. If a developer added a recursive bug to the code that caused memory usage to spike, how would your application handle it?

As for now, we would see errors in our logs system. To improve it, I should configure Alarms

11. What would happen if your database was corrupted or accidentally deleted?

Databased is backed up hourly/daily

## Performance

Might anything in your application cause user requests to fail to meet latency requirements?

It shouldn't be the case

How do you configure and optimise your compute resources? (EC2 instance type / Lambda memory)

To start with, I would set default config for Lambdas and then optimise based on the data from usage

What should the team be monitoring to ensure optimal performance?

Latency, errors,

## Cost Optimisation

1. What is the rough cost to run this application?

Based on `There are 5 initial users with between 2 and 14 rental properties each`, let's say we have 50 properties in total. Each property received an average of ~100 request per day, that would be 150000 req/month. APIs (APIGW + Lambda) are a pay as you go, we should stay in the free tier. S3 + cloudfront to host application typically is around $1-3 per month. DynamoDB based on requests + Streams should stay < $10

2. What is the most expensive component of your application?

Probably Cloudwatch Logs but I need to run the numbers to get a specific estimation

3. What designs/patterns have been implemented to optimise costs?

Serverless with Event based Architecture

## Sustainability

How does your architecture make the most of user usage patterns to improve sustainability?

# Project specific questions

1. How accurate is your scheduling method? If a visitor gets there but still hasn’t been sent the key lock code then they’ll be very annoyed. (DynamoDB TTL method for scheduling is only guaranteed to 48 hours)

Since I'm using Event bridge scheduler the accuray is around one minute.

2. What if the email to the cleaning crew fails to send? Have you overwritten the current code so no-one can unlock the key box?

Ideally, the Lambda function that send the email to the crew, will overwrite the code first and then send the email. If the email fails, I can setup a retry method OR tell the crew member to reach out through a support email and we will send them the correct code

3. If you’ve used DynamoDB, what is your schema so that you can effectively query the bookings by property or by owner?

The idea is to use Single Table design and the design is the following. Primary Key PK and Sort Key SK have general names so there will be key overloading. The first thing to do is to think about access patterns. The main ones are:

- Get Owners Profile
- Get Owners Properties
- Get Property Details
- Get Reservations Details
- Get All Reservations per Property
- Get Reservation by Guest
- Get Reservations by Start/End Date
- Get Reservation by Id

(think about access pattern)

| Entity              | PK                        | SK                                  | Attributes          | Query Example |
|---------------------|---------------------------|-------------------------------------|---------------------|---------------|
| OWNER               | OWNER_EMAIL#\<email>      | OWNER_EMAIL#\<email>                | {Owner attributes}  | PK and SK are owner email |
| RESERVATION         | RESERVATION_ID#\<id>      | RESERVATION_ID#START_DATE#\<startDate> | {Reservation attributes} | Specify reservation Id to get single reservation OR specify startDate to get all reservations per property PK = RESERVATION#\<ReservationID> AND SK BETWEEN 'START_DATE#\<date>' AND 'START_DATE#\<date>' |
| OWNER PROPERTIES    | OWNER_EMAIL#\<email>      | PROPERTY_ID#\<id>                   | {Owner Properties attributes} | PK: Owner email and returns all properties by owner's email |
| PROPERTY            | PROPERTY#\<id>            | PROPERTY#\<id>                      | {Property attributes} | PK and SK are property Id |
| PROPERTY RESERVATIONS | PROPERTY#\<id>          | RESERVATION_ID#\<id>                | {Property Reservations attributes} | PK is Property Id and returns all reservations by property Id |
| GUEST               | GUEST#\<email>            | GUEST#\<email>                      | {Guest attributes}   | PK and SK are guest email |

4. What ongoing maintenance tasks are there to maintain this app? Is this too much for the founder to handle on their own?

There shouldn't be any huge maintance processes.

5. How are you ensuring that one of the rental owners can’t access the properties and data of another owner?

I am using different User Pools in Cognito to separate auths.

6. At the requested scale the application might be over 300,000 bookings a year (400 owners, 15 properties, 50 bookings per year). How does your architecture handle this? Take note of limits in your email service provider and auth platform.

From APIs and storage point of view, it's fully scalable based on load. Email provider should be adaptable as well and auth provider is not a problem (AWS Cognito)

6. You are asked to add a feature. When there is a cancellation or a booking slot that has not been booked, the owner wants a button to send an email to all people who have previously stayed there. How complicated would it be to extend your current architecture to handle this?

Since the architecture is event based, it shouldn't take too much time. When a cancellation is triggered, I can send an email based on that event

7. A hotel chain hears about the app. They have 80 hotels, each with around 400 rooms. The hotel chain needs more fine access control. They need three new roles: chain manager, hotel manager and hotel employee. How complicated would it be to extend your current architecture to handle this?

I can create a sort of Access Control list and user roles with Cognito but need to explore the details

9. Are there any known limitations in your current architecture that could become an issue with increased scale?

There shouldn't be.
