# **Business Details**

A founder has identified a need for a Virtual Event Management platform. The target users include companies organising interactive community events and hackathons. The goal is to provide a solution for planning, hosting, and managing virtual events, including features such as event planning, virtual venue creation, ticketing, and analytics for participant engagement.

# **Requirements**

## **Functionality**

1. **Event Planning and Scheduling:**
   - Allow organizers to plan and schedule virtual events.
   - Provide a user-friendly interface for setting up event details.
   - Organisers can invite people to be co-hosts for the event.
   - Organisers can create a set of judging criteria. This means the participants know what they are going to be doing
2. **Ticketing and Registration System:**
   - Implement a ticketing system for event registration.
   - Provide options for different ticket types and pricing.
3. **Virtual Venue:**
   - There is a “virtual venues” web application for hosting events and facilitating interactive and engaging experiences.
   - Hosts can livestream a welcome video to all participants.
   - Participants can ask questions in a live chat window in the app.
4. **Hackathon Teams**
   - Organisers can send all participants into breakout teams. Organisers have a target number of participants per team.
   - Teams get their own private chat but can invite a host if they need help.
   - Hosts have a view of all teams. They can see if a team is requesting help. They can join any team conversation at that point.
5. **Team Submissions**
   - At the end of the hackathon, teams can submit their projects. This includes description and details, but also a file upload for any files required.
   - Hosts and organisers can view all submissions.
   - Submissions can be graded and participants get feedback on their submission.
6. **Analytics for Participant Engagement:**
   - Include analytics tools to track participant engagement during events.
7. **Participant Exports:**
   - Organisers can export all of the participants in csv format.
   - Organisers can connect their HubSpot or Salesforce account and sync participants automatically at the end of an event.
8. **Customisation:**
   - Allow customers to upload a logo and set two colours for branding purposes.
9. **User Roles:**
   - Define roles such as event organiser and event host.

## **Non Functional Requirements**

- The web application needs to be quick (sub 2s) and responsive but is not that latency-sensitive.
- Videos need to be streamed with sub 5s latency.
- All web pages need to be secured (https).
- Ensure the platform is GDPR compliant, adhering to data protection and privacy regulations.
- Support events with up to 500 people.
- Accommodate a total concurrency of 5000 event participants across all clients.
- Budget and Timeline**:**
  - Utilise a team of 8 developers with a target launch date of 4 months from the current date.
  - The same team will be employed to continue the development after the initial launch
- An event will cost $1 per participant for up to 4 hours or $2 for up to 24 hours
