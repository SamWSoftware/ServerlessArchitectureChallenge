### Security:

- How do you secure your data in transit?
- How do you secure your data at rest?
- How is your architecture protected against malicious intent?
  - APIs
  - Storage ( database and file storage )

### Reliability:

- How would your infra react if an availability zone went offline for an hour?
  - Would your application still be usable?
  - Would there be any temporary or permanent loss of data?
- How would your application react if your traffic increased 10x in 5 minutes? (An advert plays on tv)
  - Would your compute and database scale up to handle this quick increase in traffic
  - Might you hit some service limits?
- If a developer added a recursive bug to the code that caused memory usage to spike, how would your application handle it?
- What would happen if your database was corrupted or accidentally deleted?

### Performance:

- Might anything in your application cause user requests to fail to meet latency requirements?
- How do you configure your compute resources? (EC2 instance type / Lambda memory)
- What should the team be monitoring to ensure optimal performance?

### Cost Optimisation:

- What is the rough cost to run this application?
- What is the most expensive component of your application?
- What designs/patterns have been implemented to optimise costs?

### Sustainability:

- How does your architecture make the most of user usage patterns to improve sustainability?

### Project specific / things to watch out for

- How accurate is your scheduling method? If a visitor gets there but still hasn’t been sent the key lock code then they’ll be very annoyed. (DynamoDB TTL methods for scheduling is only guaranteed to 48 hours).
- What if the email to the cleaning crew fails to send? Have you overwritten the current code so no-one can unlock the key box?
- If you’ve used DynamoDB, what is your schema so that you can effectively query the bookings by property or by owner?
- What ongoing maintenance tasks are there to maintain this app? Is this too much for the founder to handle on their own?
- How are you ensuring that one of the rental owners can’t access the properties and data of another owner?
- At the requested scale the application might be over 300,000 bookings a year (400 owners, 15 properties, 50 bookings per year). How does your architecture handle this? Take note of limits in your email service provider and auth platform.
- You are asked to add a feature. When there is a cancellation or a booking slot that has not been booked, the owner wants a button to send an email to all people who have previously stayed there. How complicated would it be to extend your current architecture to handle this?
- A hotel chain hears about the app. They have 80 hotels, each with around 400 rooms. The hotel chain needs more fine access control. They need three new roles: chain manager, hotel manager and hotel employee.
  - How complicated would it be to extend your current architecture to handle this?
  - Are there any known limitations in your current architecture that could become an issue with increased scale?
