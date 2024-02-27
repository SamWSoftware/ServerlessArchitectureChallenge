# **Review Questions**

You’ve had a week to design some architecture, so let’s get onto reviewing it. Go through all of these questions and answer them for yourself. Some of them will be simple one or two-word answers, others will require a more detailed answer, and some may even require extra research, diagrams and notes.

Hopefully, some of these questions will highlight limitations in your architecture or ways you can improve your serverless architecture knowledge and skills. Limitations in your architecture aren’t bad - as long as you understand them, accept them and learn from them.

## **Project-specific questions/things to watch out for**

- If two people track the same channel or video, do you do the work twice?
- How many videos will you actively be tracking when at the required capacity?
- Are you creating a schedule for every video and channel or something different?
  - Are there any limitations on the number of things scheduled in your design?
- How do you efficiently tell whether a thumbnail has changed? The URL is the same even when the thumbnail changes.
- When getting analytics for a video, a lot of the time spent is fetching the website page and image. Can you use this time optimally?
- When viewing the data on a video (like the example image) how many database records are you querying?
  - Is there a way to optimise this?
  - Is this necessary?
- How are you ensuring that a user can only see the videos that they are following (or videos from channels that they follow)?
- A YouTube channel reaches out and wants more details on outlier videos. How complicated would it be to:
  - Add further processing when an outlier is found.
  - Get the transcript of the video and then use AI to summarise.
  - Run an analysis on the thumbnails, titles and summaries to find trends in overperforming videos.
- Another channel asks if you are able to do higher-resolution video tracking.
  - What is the highest resolution that you could track?

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
