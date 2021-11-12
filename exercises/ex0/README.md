# Overview

In this exercise, you will get the overview of the scenario that we are going to build in this workshop. You will also familiarise with systems and login process.

## Scenario

We will create an extension application for the SAP Sales & Service Cloud (also referred as C4C) that will provide creation and listing of simple warranty objects for a given account and its registered products. The application will be developed in the SAP AppGyver and embedded in the Sales & Service Account screen as a mashup. This will provide user to:
- See all the warranties created for an account in the C4C screen.
- Create warranties for the registered products for the account.

Note that the intenstion of this workshop is to show the techincal capbilities not on the scenario itself. 
## Techincal overview

The following diagram gives the overview of different components and services involved. The pieces that we develop in this workshop is marked with light blue border:
<br>![](/exercises/ex0/images/00_01_Overview.png)
 
The application comprises of three major parts:
- Backend service that persists the data and implements backend logic. It allows us to fetch data from **SAP Sales and Service Cloud** and expose it via REST API. This is done in the **SAP AppGyver Cloud Integrations** builder
- Frontend to create the user interface (web application) using the service interfaces created in the previous step. This is done using **SAP AppGyver Composer**
- Integrating the web-app created in the previous step to **SAP Sales and Service Cloud**

## Systems - User Selection & Login

In this step you will familiarise yourself with the systems that will be used in the workshop.

1.	AppGyver system and user.
  - Claim a user with your own email address from the URL shared during the session
  - You'll also get an email with credentials
  - These credentials will be valid until 16th December 2021.  If you wish to continue experimenting after that you are encouraged to sign-up for Free SAP AppGyver account from https://www.appgyver.com

2.	SAP Sales & Service (C4C) system and user
  - Note that we will need C4C system only to access the data via API. The UI integration steps are performed by the instructor.
  - System: https://my356925.crm.ondemand.com/
  - User/password: `DISPLAY` / `ReadMe`

## Summary

Now that you have familiarized ourself with the scenario and systems involved, let's proceed with the actual exercises.

Continue to - [Exercise 1 - Creating REST services with SAP AppGyver Cloud Integrations builder](../ex1/README.md)
