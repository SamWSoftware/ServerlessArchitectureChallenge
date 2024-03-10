# **Business Details**

Smart Tech and IoT aren’t just about automating your home lights and sprinklers. Industry has started to use it for some compelling functionality.

One industry that is changing is Green Energy. Being able to monitor and analyse both the energy generation and storage of systems can be incredibly valuable. Whether that is for a notification system for equipment issues or being able to control your system to store electricity during the day and sell it at night at a higher price.

You’ve been approached by a company that builds devices that connect to green energy systems to add IoT functionality. They have written the code for analysing the data but need a scalable way to ingest and process the data.

They will be selling this as a service to green energy projects.

# **Requirements**

## **Functionality**

- Ingest energy production events from IoT devices installed on any green energy device (solar panels, wind turbines, hydro turbines, energy storage devices eg. battery banks)
  - Devices can be set to send one event every 10s in real-time or batch 10s events and send that data once per minute.
- Detect anomalies in the outputs
  - Issues with the equipment
  - Weather anomalies
- Store data for long-term analysis and future prediction
  - Solar panel degradation
  - Battery cycle degradation
  - Predicting future energy generation capacities
  - Estimating real-world production for new projects
- Users can add devices to their account which starts the data ingestion process.
  - This involves selecting the device type, device ID and confirming a data connection
- View real-time data
  - See all of the generated power and storage capacity
  - See any anomalies
  - See future energy predictions for you system
  - View the live sell price for the energy with your respective provider
- Control devices
  - Send commands to devices
    - Store or sell electricity
    - Turn on / off turbine
  - Schedule commands
    - Charge the battery bank until 5pm then change to sell to the grid
- There can be multiple members of a project
  - owners - all permissions
  - admins - all permissions except billing
  - analyst - view only
  - engineer - view only anomalies

## **Non Functional Requirements**

- Events need to show up in the dashboard within 10s of receiving them.
- Ingest data from 2,000 real-time devices and 10,000 devices sending batches of events.
