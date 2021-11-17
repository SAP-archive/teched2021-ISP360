# Exercise 1 - Creating REST services with SAP AppGyver Cloud Integrations builder

In this exercise we will build backend services with the **SAP AppGyver**. We will build three services:

- To store and read the warranty information
- To read registered products data from SAP Sales Cloud
- To create and read warranty subscription information for given account and registered product

After completion of this exercise, you would be familiar with

- Create backend project
- Creating database tables
- Perform CRUD operations on them using REST API
- Consuming external REST endpoints (like Sales Cloud OData API)
- Deploying and testing the service

**Disclaimer:** SAP AppGyver Cloud Composer (a.k.a. Cloud Integrations) featured in this session is a pre-released product and still under development. SAP reserves the right to make changes and set a future release date or not release it at all.

## Exercise 1.1 Opening a backend project

First you will need to go to **Cloud Integrations** builder from main **SAP AppGyver** view. We have pre-created and deployed an empty project for you so we'll get a running start for the workshop. You can create a new project yourself after the workshop steps.

1. Login to backend if you haven't already
  - https://platform.testgyver.com/auth/legacy
  - Enter credentials from the *Getting Started* step

2. Click *Cloud Integrations* button
  <br>![](/exercises/ex1/images/01_11_01_Backends.png)

3. Open existing *Cloud Integration* project
  <br>![](/exercises/ex1/images/01_11_02_OpenBackend.png)

4. Once Backend is open you will see some basic information
  - Name: Name is name of the backend service/application
  - Hostname: This will be part of the API URL. Changing hostname will require removing existing deployment and deploying again so you should not change this during the workshop to avoid unnecessary wait time
  <br>![](/exercises/ex1/images/01_11_03_Config.png)

Now we will proceed with creating database tables required for our backend services.

## Exercise 1.2 Implement Warranty REST API

### Exercise 1.2.1 Create database table to store Warranties

Since we are creating an application which would show the subscribed warranties, first we need a table to store warranty details like warranty terms.

After completing these steps you will have a table to store warranties.

1. To create backend tables navigate to Data Tables options, Click on ADD NEW button. Provide a name to the table as `Warranties`

  <br>![](/exercises/ex1/images/01_12_01_CreateDataTable.png)

2. Configure Warranties table

  Once the table is created an `id` field is automatically added. This is the primary key to our database table and is a required property for creating new records. When we are creating new records to database then **SAP AppGyver** will automatically generate value for this id field.

  Add an additional table field, named `CoverageTerm` (1) as below and click plus icon (2):

  <br>![](/exercises/ex1/images/01_12_02_CreateDataField.png)

3. New field type is *Text* and it is required by default. Keep these values and click SAVE button (1) at top right corner as shown below:

  <br>![](/exercises/ex1/images/01_12_03_Save.png)

4. Scroll back up and click DATA BROWSER button

  <br>![](/exercises/ex1/images/01_12_04_DataBrowser.png)

  - Then create some warranties with coverage terms of your choosing. First time creation will take a while so wait for the blue Success message before creating another Warranty record:

  <br>![](/exercises/ex1/images/01_12_05_CreateWarrantyRecords.png)

  - Success message should look like this:

  <br>![](/exercises/ex1/images/01_12_06_CreateSuccess.png)

  - Create two or more warranties

5. Close the Data Browser modal and scroll page down and click GENERATE ENDPOINT button

  <br>![](/exercises/ex1/images/01_12_07_GenerateEndpoint.png)

### Exercise 1.2.2 Test auto-generated Warranties API

In the above section we have already created the database tables (Warranties) with some records and created Data Resource endpoint. Now we will test the auto-generated API for the first time.

1. Save the project from top right corner

2. Test the API in the browser (or postman)

  - Get the URL from the corresponding data source and operation and test it either in a web-browser or postman
  - You can see a glimpse the Logic Editor at the bottom of the screen. We'll come back to it later

  <br>![](/exercises/ex1/images/01_12_09_CopyURL.png)

  - If you paste the URL to browser it will return a JSON response like this:

  <br>![](/exercises/ex1/images/01_12_10_Test.png)

## Exercise 1.3 Consuming a SAP Sales Cloud API in the SAP AppGyver backend

  In the next step we need to implement an API to create, read, update and delete warranty description. However, before that we need an API to read registered products. We will read the registered producs from the SAP Sales Cloud system. However, we can't use the SAP Sales Cloud API directly in a AppGyver UI application directly due to CORS (Cross Origin Resource Sharing) issue. So, we need to wrap the SAP Sales Cloud API inside a AppGyver backend API. In this section we will do the same.

1. Click BACK from left side menu and navigate to the EXTERNAL RESOURCES section to create a new OData Resource:

  <br>![](/exercises/ex1/images/01_12_11_Back.png)

  - Click ADD ODATARESOURCE button:

  <br>![](/exercises/ex1/images/01_13_01_ODataResource.png)

2. Add following configuration to do discover available resources from SAP Sales Cloud API
  - Choose `Basic Authentication`
  - Username `DISPLAY`
  - Password `ReadMe`
  - Base URL `https://my356925.crm.ondemand.com/sap/c4c/odata/v1/c4codataapi/`
  - Click VERIFY URL button and wait for a while

  <br>![](/exercises/ex1/images/01_13_02_ODataResource.png)

  - You will see long list of available resources to make selection easier you can filter it
  - Write 'RegisteredProductParty' to filter field (1) and toggle on 'RegisteredProductPartyInformationCollection' (2)

  <br>![](/exercises/ex1/images/01_13_03_ODataResource.png)

  - Expand 'RegisteredProduct'

  <br>![](/exercises/ex1/images/01_13_04_ODataResource.png)

  - You can test how the results look from TEST tab
  - Click SAVE DATA RESOURCE after you've done the test

  <br>![](/exercises/ex1/images/01_13_05_ODataResource.png)
  <br>![](/exercises/ex1/images/01_13_06_ODataResource.png)

3. Click GENERATE ENDPOINT to create Date Resource from OData API

  <br>![](/exercises/ex1/images/01_13_07_GenerateEndpoint.png)

4. Save (1) and change output schemas:

  <br>![](/exercises/ex1/images/01_13_07b_Save.png)

  - Navigate to the GET COLLECTION (1)
  - Toggle off (2) to return specified properties
  - Toggle every except 'RegisteredProductID' off (3)

  <br>![](/exercises/ex1/images/01_13_07c_Output.png)

5. Scroll down to Logic Editor and double-click List Records block

  <br>![](/exercises/ex1/images/01_13_08_ConfigureListRecords.png)

  - Click 'Authconfig' value bind button:

  <br>![](/exercises/ex1/images/01_13_09_ConfigureListRecords.png)

  - Choose 'Object with properties':

  <br>![](/exercises/ex1/images/01_13_10_ConfigureListRecords.png)

  - Choose 'Basic' authentication
  - Click 'Username' value bind button

  <br>![](/exercises/ex1/images/01_13_11_ConfigureListRecords.png)

  - Choose 'Static text'
  - Repeat same for 'Password'

  <br>![](/exercises/ex1/images/01_13_12_ConfigureListRecords.png)

  - Type `DISPLAY` to Username value
  - Type `ReadMe` to Password value
  - Click SAVE button to close the modal

  <br>![](/exercises/ex1/images/01_13_13_ConfigureListRecords.png)

6. In the Logic Editor, click 'Send Successful Response' block and change response to a Formula:
  ```
  MAP<Record>(outputs["List records"].records,  { RegisteredProductID: Record.RegisteredProductID + ":" + Record.RegisteredProduct.SerialID })
  ```

  - Click 'Response data' value bind button:

  <br>![](/exercises/ex1/images/01_13_14_Response.png)

  - Choose 'Formula'

  <br>![](/exercises/ex1/images/01_13_15_Response.png)

  - Click existing formula to edit it:

  <br>![](/exercises/ex1/images/01_13_16_Response.png)

  - Replace existing formula with a `MAP` formula from above in exercise:

  <br>![](/exercises/ex1/images/01_13_17_Response.png)

7. Save the project from top right corner and test new endpoint:
  - Copy the URL from following location
  - Ie. `https://<your unique hostname>.cm-backends.testgyver.com/api/v1/registeredproductpartyinformationcollection/`

  <br>![](/exercises/ex1/images/01_13_19_TestURL.png)

  - You should see a lot of registered products with above mapping data

  <br>![](/exercises/ex1/images/01_13_20_Safari.png)

## Exercise 1.4 Implementing Warranty Subscription API

In the Exercise 1.2 we have already create a table to store Warranties and implemented an API to read from the table. In this section we will create a table to store the Warranty Subscriptions and API for list and create operations.

### Exercise 1.4.1 Create Warrant Subscription Table

1.	To created backend tables navigate to Data Tables options, Click on ADD NEW. Provide a name to the table as 'WarrantySubscriptions'.

  <br>![](/exercises/ex1/images/01_14_01_AddSubscriptionTable.png)

2.	Configure Warranty Subscription table

  - Once the table is created, as we have seen earlier, an `id` field is automatically added, which will be the primary key to our database table
  - Add additional table fields as below:

| Field name | Type | Description |
| ---------- | ---- | ----------- |
| IsActive | True/false | To check if the warranty is in active status or not |
| Product | Text | To show the registered product description for selected account |
| AccountID | Text | Account ID |
| WarrantyEnd | Date text - ISO 8601 | Warranty expiry date information |
| WarrantyID | Text | Warranty ID |

  - Scroll down and “Add New Property” to add fields as shown below:

  <br>![](/exercises/ex1/images/01_14_02_AddField.png)

  - Example of `IsActive` is given below:

  <br>![](/exercises/ex1/images/01_14_03_FieldConfig.png)

  - Please configure other fields in the same way

3. Scroll to the bottom of the page and click GENERATE ENDPOINT button

  <br>![](/exercises/ex1/images/01_14_04_GenerateEndpoint.png)

4. Save project from top right corner

5. Choose GET COLLECTION from left side. Now it's time to familiarise ourselves with the Logic Editor

  <br>![](/exercises/ex1/images/01_14_05_LogicEditor.png)

  - Choose existing 'List Records' node (1) from the canvas and move it around freely
  - Open 'Advanced' tab (2) from right side 'Properties' and rename node to 'List Subscriptions' (3)

  <br>![](/exercises/ex1/images/01_14_06_RenameListRecords.png)

  - Drag new 'List Records' node under 'Data Tables' section to Logic Editor (1)
  - Notice that left side menu also has 'List Records' under 'External Resources'! Use 'Data Tables' option instead
  - Choose existing wires from 'List Subscriptions' to response nodes and delete them. Use Backspace key with Mac and Windows:

  <br>![](/exercises/ex1/images/01_14_07_DragNode.png)

  - Connect 'List Subscriptions' top output wire to new 'List Records' input (1)
  - Connect new 'List Records' output wire to existing response nodes inputs (2, 3)
  - Rename new 'List Records' to 'List Warranties' and make sure it is connected to 'Warranties' table (4, 5)

  <br>![](/exercises/ex1/images/01_14_08_RenameListWarranties.png)

6. Join Coverage Terms from Warranties to Warranty Subscriptions by using a mapping function in response node

  - Click 'Send successful response' node and click 'Response data' value bind from Properties

  <br>![](/exercises/ex1/images/01_14_16_SetResponseFormula.png)

  - Choose 'Formula'

  <br>![](/exercises/ex1/images/01_14_17_ChooseFormula.png)

  - Click existing formula to edit it:

  <br>![](/exercises/ex1/images/01_14_18_ChangeFormula.png)

  - This Formula goes through each Warranty Subscriptions and finds a matching Warranty from Warranties
  - It then adds `CoverageTerm` from the Warranty to output
  - Copy Formula to it's place:
  ```
  MAP<Subscription>(outputs["List Subscriptions"].records, MERGE([Subscription, { CoverageTerm: FIND<Warranty>(outputs["List Warranties"].records, Warranty.id == Subscription.WarrantyID).CoverageTerm }]))
  ```

  <br>![](/exercises/ex1/images/01_14_19_MapFormula.png)

  - Click SAVE

7. Add `CoverageTerm` to the output schema

  - Navigate back to BASE CONFIGURATION (1) and scroll to the bottom of the page
  - Add new field called `CoverageTerm` (2) and click plus icon (3)

  <br>![](/exercises/ex1/images/01_14_20_SchemaChange.png)

  With this we have implemented Get Collection to get the list of warranty subscriptions. Now let us implement Create Warranty Subscription to create some records before testing it.

### Exercise 1.4.2 Create Warranty Subscriptions.

1. Save the project

2. To test go back to Data Resources and choose WarrantySubscriptions

  - To test we need to use some tools that can post the data. In this workshop we will use [Postman](https://www.postman.com/downloads/)
  - Run 'GET warranties' end point Exercise 1.2.2 to get some valid Warranty IDs. These will be used to create warranty-subscriptions
    - Ie. `https://<your unique hostname>.cm-backends.testgyver.com/api/v1/warranties/`
  - Run  'POST warrantysubscriptions' end point and provide following payload
    - Ie. `https://<your unique hostname>.cm-backends.testgyver.com/api/v1/warrantysubscriptions/`

  ```json
  {
    "Product": "1001",
    "IsActive": true,
    "AccountID": "1000034",
    "WarrantyID": "<replace with an warranty-id in the previous step>",
    "WarrantyEnd": "2021-11-16"
  }
  ```
  <br>![](/exercises/ex1/images/01_14_24_TestPost.png)

  - Test 'GET warrantysubscription' end point by replacing POST with GET action in the URL bar.

## Summary

In this section we have created three backend service APIs that will be used to build the user interface in the next section. We have built APIs based on the local storage as well as created wrapper API by consuming an external API (SAP Sales Cloud Registered Product).

Continue to - [Exercise 2 - Building the UI with the SAP AppGyver Composer](../ex2/README.md)

