# Breezy + HubSpot Integration POC

This project is a proof-of-concept (POC) backend + frontend integration showing how your company **Breezy**, a smart thermostat company, could sync customer data and subscription activity into **HubSpot** using the CRM API.

The app includes:

- An Express.js backend that proxies to HubSpot
- A simple browser-based frontend (`/public/frontend.html`)
- Flows to:
  - Sync customers as HubSpot **contacts**
  - Track subscription conversions as HubSpot **deals**
  - View deals (subscriptions) per contact
- A documented data model & pipeline design for Breezy’s HubSpot architecture

---

## A. Setup Instructions
1. Running the Application Locally

This project consists of two components:

Frontend (static HTML/JS application you extend)

Backend (Node/Express server connecting to HubSpot’s APIs)

To run locally:

Clone the repository:

git clone <https://github.com/kgibson922-dev/hs-solution-architect-tech-assignment-main-test.git>
cd breezy-hubspot-poc


Install backend dependencies:

cd backend
npm install


Start the backend:

npm start


You should see the server running on:
http://localhost:3001

Open the frontend:

Either open frontend.html directly in your browser -- if this doesn't work go to http://localhost:3001/frontend.html

2. Dependencies / Prerequisites

Node.js v18+ (required to support native fetch)

npm

HubSpot Private App Token with:

CRM Read/Write permissions for Contacts

CRM Read/Write permissions for Deals

Browser supporting ES6 modules

3. Required Environment Variables

Create a .env file in the backend directory:

Variable	Description
HUBSPOT_PRIVATE_APP_TOKEN	Token for HubSpot API requests 
Example: HUBSPOT_PRIVATE_APP_TOKEN=pat-xxxxxx

4. How to Test the Integration Flow

Create a Contact from the frontend UI
→ Should POST to /api/contacts → HubSpot CRM

View Contacts List
→ Should GET from /api/contacts (proxying HubSpot search endpoint)

Create a Deal for a contact
→ Should POST to /api/deals with associations

View Deals for a Contact
→ Should GET from /api/contacts/:id/deals

B. Project Overview

This Proof of Concept showcases how Breezy’s applicant data could integrate seamlessly into HubSpot CRM.
It demonstrates:

Syncing candidate/contact data from Breezy → HubSpot

Automatically generating deals representing hiring stages

Presenting contacts, deals, and related CRM data in a clean frontend

Adding an AI-driven enhancement to improve recruiter productivity

The POC is intentionally lightweight but models the architecture needed for a production-ready integration.

C. AI Usage Documentation 
AI was used across this assessment task. It was used to get started with GitHub. It was also used to develop code for the frontend.html file and troubleshoot leveraging Github as there were hurdles. In terms of learnings, the overall task and conversation in this scenario feels familiar, but the challenge was rooted in getting started with a toolset I'm not as familiar with in the asks of my current job function as a CSM. It's humbling entering tools and needing to learn how to make them function -- truthfully it is a good reminder to bear in mind working day in and day out with customers. AI really allowed me get my bearings and from there I was able to lean on experience to work on the task at hand in discovering and solving for this customer.   

D. Data Architecture is include in the Screenshot Folder labeled ERD - Tech Assessment Diagram 
Business Flow: A contact comes into the system when they purchase a Thermostate. That purcahse should be reflected as a Deal in a specific pipeline to enable revenue tracking, reporting, and segmenation effort. Information about the actual Thermostate should also be captured on a custom object should warranty or recall information be necessary. From there, if a Contact activates a trial or purchases a subscription outright following their  Hardware purchase that should be captured in a separate pipeline. This is where with deal stages there is an ability to capture conversion through deal stages, but also the overall close won revenue Breezy is capturing on the SaaS side of the business.
Association relationships include: 
Contact <> Thermostat:  One Contact can be associated to many thermostats, but a themostat can only be associated to one contact. 
Reason: A contact can be associated to multiple thermostats because they could have mulltiple homes or there could need to be serveral themostats installed in their home depending on their HVAC set up 

Contact <> Hardware Purchase Deal:  One contact can be associated to multiple Hardware Purchase Deals. For simliar reasons above a contact may purchase multiple thermostats for multiple homes, for their HVAC setup or overtime an existing thermostat may break and need replacing 

Contact <> Subscription Deals:  One contact can be associated to multiple Subscription Purchase Deals, but the subscription will be assocaited to one contact. The rationale here is again there may be a need to purchase multiple subscriptions for different locations or a contact may purchase, churn and then return to subscribing agan. 

Harware Purchase Deal  <> Thermostat:  In this specific case a Themostat can only be associated with a single deal, but a deal could contain a quantity of one or multiple themostats. 

F. Design Decsions 
Assumptions made include the fact that Breezy is collecting information on the hardware 

In terms of additional information that would be helpful from the  client: 
What are the key questions you are looking to answer on the HubSpot side? 

Do subscriptions last for a designated amount of time (have an end date) or do they run until cancelled. This would also inform whether a renewal process would be relevant 

From a goal and business perspective, are we looking to have Breezy or HubSpot function as a source of truth? This could help inform whether the integration is one direction or bi-directional. 


