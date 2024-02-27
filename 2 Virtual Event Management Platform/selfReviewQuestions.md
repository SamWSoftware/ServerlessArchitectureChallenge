# **Review Questions**

You’ve had a week to design some architecture, so let’s get onto reviewing it. Go through all of these questions and answer them for yourself. Some of them will be simple one or two-word answers, others will require a more detailed answer, and some may even require extra research, diagrams and notes.

Hopefully, some of these questions will highlight limitations in your architecture or ways you can improve your serverless architecture knowledge and skills. Limitations in your architecture aren’t bad - as long as you understand them and accept them.

## **Project specific questions / things to watch out for**

- How are you ensuring GDPR compliance?
  - Explicit authorisation to store and use data
  - Personal Data Security (storage and protection from unauthorised access)
  - Ability to request data
  - Ability to request the deletion or anonymisation of any of their data
- What is the latency on the video solution you’ve gone with?
- If a user disconnects from any of the chats (main or team) will they be able to get the message history
- Are there any limitations on the number of participants in the event? Some video streaming tools have a limit on the number of connections
- How ‘real time’ will your analytics be?
- How are you tracking the number of participants who joined an event? How certain are you that there won’t be missed or double counts? This is used for billing!
- You have a busy weekend and hit 5000 concurrent participants. Estimate that they are each sending 2 messages / min. Will this be an issue for your application?
- You are asked to add a feature. Video chat for breakout teams. How difficult would it be to implement a feature like this?
- A large company wants to do a company-wide hackathon. They have 15,000 staff. They want users to be able to log into the event using their company credentials. You still need to support other customers whilst this event is happening
  - How complicated would it be to extend your current architecture to handle this?
  - Are there any known limitations in your current architecture that could become an issue with increased scale?

## **Default Questions (Well-Architected Framework)**

To start we have a set of questions that are generic to any type of architecture, serverless or not. These questions will be part of every self-review and are a great starting point. If there are any other questions you’d add to this list, send them over to me!

### **Security:**

- How do you secure your data in transit?
- How do you secure your data at rest?
- How is your architecture protected against malicious intent?
  - APIs
  - Storage ( database and file storage )

### **Reliability:**

- How would your infra react if an availability zone went offline for an hour?
  - Would your application still be usable?
  - Would there be any temporary or permanent loss of data?
  - Would that be acceptable?
- How would your infra react if a whole region went offline for an hour?
  - Would your application still be usable?
  - Would there be any temporary or permanent loss of data?
  - Would that be acceptable?
- How would your application react if your traffic increased 10x in 5 minutes? (An advert plays on tv)
  - Would your compute and database scale up to handle this quick increase in traffic
  - Might you hit some service limits?
- If a developer added a recursive bug to the code that caused memory usage to spike, how would your application handle it?
- What would happen if your database was corrupted or accidentally deleted?

### **Performance:**

- Might anything in your application cause user requests to fail to meet latency requirements?
- How do you configure and optimise your compute resources? (EC2 instance type / Lambda memory)
- What should the team be monitoring to ensure optimal performance?

### **Cost Optimisation:**

- What is the rough cost to run this application?
- What is the most expensive component of your application?
- What designs/patterns have been implemented to optimise costs?
- What optimisations could be made to your architecture if the scale requirements were 100x?

### **Sustainability:**

- How does your architecture make the most of user usage patterns to improve sustainability?
