# Serverless Architecture Challenge #1

# Designing a Holiday Rental Property Management Tool

## Business Details

A founder has been contacted by a woman who runs a holiday rental business. She has 8 properties and is tired of trying to schedule and organise all of the properties using Google Calendars and trying to remember to manually email everyone involved.

The founder then found 4 other holiday rental owners who struggle with similar issues and would love an app to handle bookings and communication for visitors and staff (cleaners, repair, etc). They need an app to be able to integrate into the common holiday rental platforms (booking.com, airbnb, etc). Owners would also like a site where visitors are able to view all of their properties and rent them directly.

One problem that most of these property owners have is managing communication with visitors and staff (cleaning team, repairs etc).

The founder has asked you to design an application that can handle the holiday rentals for all of these people.

## Requirements

### Functionality

- Ability to manage properties.

  - CRUD for a set of text-based attributes, but also store a set of images for the property.

  - Ability to manage the calendar for a given property. Owners can view the current bookings, set prices for future dates, and block dates where the property is unavailable.

  - When any of these changes are made, they are distributed into the connected holiday rental platforms.

  - There needs to be controls so that property owners can’t access each other’s properties. Property owners can invite other people to help manage the properties in the app.

- You can connect the application to the top 3 holiday rental platforms.

  - They each have an API which allows you to post changes to their system. Changes include property details, availability or communication with the visitor. These APIs are secured with an API key.

  - They all allow you to give them a webhook endpoint where they can send booking details. You can validate API events with a secret stored in the payload, which you provide in their app.

- Each property owner gets their own sub-domain site. (eg. https://myname.holidaymaster.com)

  - Users can select their own sub-domain when they sign up.

  - They connect their Stripe account so the app can pay them for direct bookings.

- Visitor booking process

  - Visitors can book through one of the three holiday rental platforms (if the owner has signed up for them).

  - Visitors can also book directly on the sub-domain site. Payments for this are handled by Stripe Connect.

  - Visitors get a booking confirmation, no matter which platform made the booking.

  - Cleaners need to be booked for the afternoon when the visitors leave. Assume there is an API for making that booking. They also need to be cancelled if a booking is cancelled.

  - 10 days before the start of the visit, the visitors get a reminder email of their trip and the 7-day cancellation period.

  - After the visit, the cleaners confirm the property wasn’t damaged and then the visitors get an email asking for a review on their recently visited property.

- All properties have key boxes with code locks.

  - The visitors need to be sent the code the day that they check in to the property.

  - To stop people coming back later and accessing the property, the code is changed after every visitor. This code needs to be sent to the cleaning crew so they can change it, along with the current code to access the property.

### Non Functional Requirements

- The web application needs to be quick (sub 2s) and responsive, but is not that latency sensitive.

- All web pages need to be secured (https).

- There are 5 initial users with between 2 and 14 rental properties each. The founder aims to scale this to hundreds of property owners with up to 50 rentals each.

- The founder has some technical skills but will be hiring a small team of freelancers to build the application you design. Initially, the founder will support it after v1 until revenue is at a level where a small team can be hired.

- The base pricing will be per property and set at $50/month. There is also a 5% fee for bookings made through our pages.

## What Happens Next?

Once you’ve designed your architecture, you want to be able to critique it. The best way is to have another architect review it. The next best thing is to have a set of questions to go through and see how your architecture answers those questions. You might find areas where your architecture could be improved and better meet the requirements.

But you’re not getting those questions just yet. I want to give you a chance to design your architecture without being influenced by the questions. You’ll get these questions in 7 days, so get architecting!

If you’re doing this challenge with a friend or colleague, that’s amazing. Peer feedback and having someone else’s viewpoints can be incredibly valuable. If you can, try and complete your architecture before reviewing and comparing it. This will help you understand the topics you know well and the ones you can work on.

If you like the idea of this Serverless Architecture Challenge then please share it with your friends and colleagues.

If you have any feedback, please email me at sam@completecoding.io

Good luck!

Sam
