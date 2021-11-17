# Overview

In this exercise, you will get the overview of the scenario that we are going to build in this workshop. You will also familiarise with systems and login process.

## SAP Sales & Service Cloud Extensibility Overview

Before starting the exercises, let us have a quick overview of the different extension options in the SAP Sales & Service Cloud. Please note that this is not an exhaustive list but just to give an idea about what part we are going to cover today. Below diagram lists two broad category of extensions:
- **In-App extensions** are the extensions that are built on the technology stack of SAP Sales & Service Cloud. These extensions are primarily needed where transaction boundaries needs to be coupled with SAP Sales & Service objects. 
- **Side-by-Side Extensions** are those that built outside the technology stack of SAP Sales & Service cloud and are loosely coupled with SAP Sales & Service applications. In this workshop we mainly build a side-by-side extension.

<br>![](/exercises/ex0/images/00_00_SalesCloudExtFeartures.png)
 
## Extending SAP Cloud for Customer with SAP Business Technology Platform
<br>![](/exercises/ex0/images/00_00_SalesCloudOverview.png)

## Scenario

We will create an extension application for the **SAP Sales Cloud** that will provide creation and listing of simple warranty objects for a given account and its registered products. The application will be developed in the **SAP AppGyver** and embedded in the Account screen of **SAP Sales Cloud** as a mashup. This will provide user to:
- See all the warranties created for an account.
- Create warranties for the registered products for the account.

Note that the intention of this workshop is to show the technical capabilities not the end product itself. 

## Techincal overview

The following diagram gives the overview of different components and services involved. The pieces that we develop in this workshop is marked with light blue border:

<br>![](/exercises/ex0/images/00_01_Overview.png)
 
The application comprises of three major parts:
- Backend service that persists the data and implements backend logic. It allows us to fetch data from **SAP Sales Cloud** and expose it via REST API. This is done in the **SAP AppGyver Cloud Integrations** builder
- Frontend to create the user interface (web application) using the service interfaces created in the previous step. This is done using **SAP AppGyver Composer**
- Integrating the web-app created in the previous step to **SAP Sales Cloud**. Note that in this workshop this part is showcased by the instructor only.

**Disclaimer:** SAP AppGyver Cloud Composer (a.k.a. Cloud Integrations) featured in this session is a pre-released product and still under development. SAP reserves the right to make changes and set a future release date or not release it at all.

## Systems - User Selection & Login

In this step you will familiarise yourself with the systems that will be used in the workshop.

1.	AppGyver system and user.
  - Claim a user with your own email address from the URL shared during the session
  - You'll also get an email with credentials
  - These credentials will be valid until 16th December 2021.  If you wish to continue experimenting after that you are encouraged to sign-up for Free SAP AppGyver account from https://www.appgyver.com

2.	SAP Sales Cloud system and user
  - Note that we will need SAP Sales Cloud system only to access the data via API.
  - System: https://my356925.crm.ondemand.com/
  - User/password: `DISPLAY` / `ReadMe`

## Summary

Now that you have familiarized ourself with the scenario and systems involved, let's proceed with the actual exercises.

Continue to - [Exercise 1 - Creating REST services with SAP AppGyver Cloud Integrations builder](../ex1/README.md)
