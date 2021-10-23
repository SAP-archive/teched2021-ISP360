# Exercise 1 - Creating REST services with AppGyver backedn builder

In this exercise we will build back-end services in the AppGyver. We will build three services:
- To store and read the warranty information.
- To read registered products data from C4C.
- To create and read warranty subscription information for given account and registered product.
 
After completion of this exercise, you would be familiar with 
- Create backend project.
- Creating database table.
- Perform CRUD operations on them usin REST API.
- Consuming external REST endpoints (like C4C OData API)
- Deploying the service.

## Exercise 1.1 Creating backend project
First you need to create a project to start implementiing the functionality.

After completing these steps you will have backend project ready to implement a REST service

1. Login to backend 
  - TODO - link to the final systems
  - Enter alloted credentials

1. Click here.
  <br>![](/exercises/ex1/images/01_11_01_createBackend.png)

2.	Once backend is created, provide a unique name and change the basic configuration. 
  - Name: Name is name of the backend service/application. **Please prefix the project name with the userid to make it unique**.
  - Hostname: This will be part of the API url path. Again please append userid with your host name like (USER-Id)-productwarranty. Note: the maximum length of this field is 20 character.
  <br>![](/exercises/ex1/images/01_11_02_projectBasicConfig.png)

  Once these base configurations are done, we will proceed with creating database tables required for our back-end services.

## Exercise 1.2 Implement Warranty REST API
### Exercise 1.2.1 Create database table to store Warranties
Since we are creating an application which would show the subscribed warranties, first we need a table to store warranty details like warranty terms.

After completing these steps you will have a table to store warranties.

1.	To created backend tables navigate to Data Tables options, Click on ADD NEW. Provide a name to the table as 'Warranty'.

  <br>![](/exercises/ex1/images/01_12_01_CreateDataTable.png)

2.	Configure Warranty Subscription table
  Once the table is created an “id” field is automatically added, which will be the primary key to our database table and is a required property while creating the data. When we are creating any instances in database the appgyver automatically generated value for this ID field and stores the data. We can change the property of the id field; the default will be as text type.

  Add an additional table field, named 'CoverageTerms' as below:

  <br>![](/exercises/ex1/images/01_12_02_CreateDataField.png)

  Please configure the field properties as below:
  <br>![](/exercises/ex1/images/01_12_03_ConfigureDataField.png)

### Exercise 1.2.2 Create a Data Source and API for getting warranty collection

In the above section we have already created the database tables (Warranty), now here we will create data resources to fetch the data from the table.

1. Navigate to Data Resources option and create one, provide the name “Warranties”, this is to get the available warranties .
  <br>![](/exercises/ex1/images/01_12_04_CreateDataSource.png)

3. Implement Get Collection
This end point will provide list of records from Warranty table.
  - Click on Get Collection
  - In the logic editor, drag & drop the "List Records" flow from the toolbar
  - Delete the JS Block that was created by default
  - Connect the output of the Request Received block to the List Records as in the belew diagrams
  - Connect the output of the List Records block to the Send Successful Response block as in the below diagram
  <br>![](/exercises/ex1/images/01_12_06_GetDSCollection.png)
 
4. Make sure the output of the response is set to the output of List Records.
  <br>![](/exercises/ex1/images/01_12_07_SetResponseList.png)

  Then select the List of Records as below:
  <br>![](/exercises/ex1/images/01_12_07a_SetResponseList.png)

4. Create some warranty records
  Now we have already implemented the get collection end point. We can already execute it. However, there is no data created yet. So let us create some data in warany table. Note that we dont have to expose any interface of that - we can just create the entries manually.
  - In the logic editor drag and drop the create record as below and click on the Create Record
  <br>![](/exercises/ex1/images/01_12_08_CreateWarrantyTableEntry.png)

  - Click on the Custom Object
  <br>![](/exercises/ex1/images/01_12_09_CreateWarrantyTablePopup.png)

  - Enter the value and Save
  <br>![](/exercises/ex1/images/01_12_10_CreateWarrantyTableValue.png)

  - Repeat the previous two steps to create more records

  5. First Deployment
  Go back and click deployment.
  <br>![](/exercises/ex1/images/01_12_11_GoToDeployment.png)
  <br>![](/exercises/ex1/images/01_12_12_FirstDeploy.png)

6. Test the API in the brower (or postman)
  Get the url from the corresponding data source and operation and test it either in a web-browser or postman.
  <br>![](/exercises/ex1/images/01_12_13_TestURL.png)

## Exercise 1.3 Consuming a C4C API in the AppGyver backend
  In the next step we need to implement an API to create, read, update and delete warranty description. However, before that we need an API to read registered products. We will read the registered producs from C4C system. However, we cant use the C4C API directly in a AppGuver UI application directly due to CORS (Cross Origin Resource Sharing) issue. So, we need to wrap the C4C APi inside a AppGyver backend API. In this section we will do the same. 

1. Nagigate to the DATA RESOURCES section and create a new data resource. Give it a name: 'RegisteredProducts'.
  <br>![](/exercises/ex1/images/01_13_01_RegProductsDS.png)

2. Navigate to the GET COLLECTION option, since we want to get all the registered product information for a particular account, we would require the account information. So, let’s add a parameter to our API to receive account id from consumer and use the same while calling the above REST endpoint.
  <br>![](/exercises/ex1/images/01_13_02_RegProductsQueryParam.png)

3. In the Logic Editor, drag and drop the “HTTP JSON request” from the toolbar and connects the blocks as following:
  <br>![](/exercises/ex1/images/01_13_03_RegProductsDSLogic.png)

4. Click on the `HTTP JSON Request` block and configure it as below:
  - In the PROPERTIES section, in the URL, click on the ABC block and choose Formula option, click on the formula input field. It navigate to next screen where in the quotes provide the `https://my356925.crm.ondemand.com/sap/c4c/odata/v1/c4codataapi/RegisteredProductPartyInformationCollection`. 
  - Save the configuration.     
  <br>![](/exercises/ex1/images/01_13_04_RegProductC4CURL.png)
  <br>![](/exercises/ex1/images/01_13_05_SelectFormula.png)
  <br>![](/exercises/ex1/images/01_13_06_RegProductFormulaURL.png)

  - In the PROPERTIES section again, set Method as 'Get' 
  - Set URL Query Parameteters: Click on 'X' box, next to it and navigate to formula editor (as for URL) and enter the value (inside double quote): 
  `[{name: "$filter", value: "PartyID eq " + request.parameters.AccountID + " and RoleCode eq '60'"}, {name:"$expand", value:"RegisteredProduct"}, {name:"$select", value:"RegisteredProductID,PartyID,RegisteredProduct/SerialID"}]`.
    
  If we see closely then in this formula we are sending a “$filter” where PartyID is the AccountID passed as the query parameters. RoleCode is the fixed value for the role type 'Customer'. We are expanding to the RegisteredProduct node to get SerialID field.
  <br>![](/exercises/ex1/images/01_13_06_SetMethodAndFilter.png)

  - Headers: For this, in place of formula editor we will use 'List of values' option. Here we set the 'Accept' header to accept 'application/json' format. 
  <br>![](/exercises/ex1/images/01_13_07_RegProductSetHeader.png)
  <br>![](/exercises/ex1/images/01_13_08_SelectListOfValues.png)
  <br>![](/exercises/ex1/images/01_13_09_HeaderEnterValues.png)

  - Authentication Credentials: Scroll down to the authorization credentials, click on the 'X' box and then 'Object with properties'. Enter the value: User Name: `Display` and password: `ReadMe`. Note that this user has limited access to just read registered products'  
  <br>![](/exercises/ex1/images/01_13_09a_Authentication.png)

5. Double click the 'JS Create Response' block and configure it as below:
  - In the Input, provide as name 'resultOfGetProducts' (as the name suggest, it is to refer the output of the previous block)
  <br>![](/exercises/ex1/images/01_13_10_NameHttpRespOutput.png)

  - Click on the 'ABC' in the resulting screen and choose the value as below
  <br>![](/exercises/ex1/images/01_13_11_SelectHttpResp1.png)
  <br>![](/exercises/ex1/images/01_13_12_SelectHttpResp2.png)
  <br>![](/exercises/ex1/images/01_13_13_SelectHttpResp3.png)

  - Copy the following Java Script code in the middle
  ```javascript
  let results = inputs.resultOfGetProducts.d.results;
  let registeredProductIds = [];
  for (let i = 0; i< results.length; i++){
    let registeredProductID = results[i].RegisteredProductID + ":" 
                  + results[i].RegisteredProduct.SerialID;
    registeredProductIds.push( {"RegisteredProductID": registeredProductID} )
  }
  return [0, {
    response: {
      message: registeredProductIds
    },
  }];
    
  ``` 
  - And confure the output (on the right hand side) as 'List' and List Item Type as 'Object':
  <br>![](/exercises/ex1/images/01_13_14_SetJSOutput.png)

  - Restart the application: 
    - Press BACK in the left navigation
    - Click DEPLOYMENTS and then RESTART button 
    - Test - copy the URL from follwoing location and paste in the browser
  <br>![](/exercises/ex1/images/01_13_15_TestURL.png)

## Exercise 1.4 Implementing Warranty Subscription API
  In the Exercise 1.2 we have already create a table to store warranties and implemented an API to read from the table. In this section we will create a table to store the warranty subscriptions and API for get and post operations.

### Create Warrant Subscription Table

1.	To created backend tables navigate to Data Tables options, Click on ADD NEW. Provide a name to the table as 'Warranty'.

  <br>![](/exercises/ex1/images/01_14_01_AddSubscriptionTable.png)

2.	Configure Warranty Subscription table

  Once the table is created, as we have seen earlier, an “id” field is automatically added, which will be the primary key to our database table. 

  Add additional table fields as below:

  Following will be the fields we will be adding to our data base table. Scroll down and “Add New Property” to add fields as shown below. Example of IsActive is given below:
  -	IsActive 	(type: True/false)	– To check if the warranty is in active status or not.
  -	Product	 	(type: Text)	– To show the registered product description for selected account
  -	AccountID (type: Text)		– Account information
  -	WarrantyEnd (type: Date text - ISO 8601 )		– Warranty expiry date information
  -	WarrantyID (type: Text)	– Warranty ID   
  <br>![](/exercises/ex1/images/01_14_02_AddField.png)
  <br>![](/exercises/ex1/images/01_14_03_FieldConfig.png)
  <br> Please cofigure other fields in the same way.

### Create Warrant Subscription Data Source and API
  1. Create Data Source
  <br>![](/exercises/ex1/images/01_14_04_CreateDataSource.png)

  2. Configure query paramter to filter based on AccountID 
  <br>![](/exercises/ex1/images/01_14_05_SetQueryParam.png)
  <br>![](/exercises/ex1/images/01_14_06_SetQueryParam2.png)

  3. Set Data Source implementation flow
  <br>![](/exercises/ex1/images/01_14_07_SetDSFlow.png) 

  4. Configure List Subscriptions:
  Double click on the 'List Subscriptions' block and configure as following:
  - Set the table as `WarrantySubscription`
  - Set filter condition
  <br>![](/exercises/ex1/images/01_14_08_SetTableFilter.png) 
  <br>![](/exercises/ex1/images/01_14_09_SetTableFilter2.png) 
  <br>![](/exercises/ex1/images/01_14_10_SetTableFilter3.png) 
  <br>![](/exercises/ex1/images/01_14_11_SetTableFilter4.png) 
  <br>![](/exercises/ex1/images/01_14_12_SetTableFilter5.png) 
  <br>![](/exercises/ex1/images/01_14_13_SetTableFilter6.png) 
  <br>![](/exercises/ex1/images/01_14_14_SetTableFilter7.png) 
  <br>![](/exercises/ex1/images/01_14_15_SetTableFilter8.png) 

  - Configure 'List Warranties' block
  <br>![](/exercises/ex1/images/01_14_16_SetWarrantyTable.png)

  - Set JS - Create Response block as below
  <br>![](/exercises/ex1/images/01_14_17_SetJSBlock.png)
  
    - Configure two input variables
      - Warranties (List of Warraties / List of records)
      - Subscriptions (List of Subscriptions / List of records)
    - Copy below JS snippet to JavaScript block:
    ```javascript
      let subscriptions = inputs.subscriptions;
      let registeredProductIds = [];
      for (let i = 0; i< subscriptions.length; i++){
        let warranty = inputs.warranties.find(item => {
            return item.id === subscriptions[i].WarrantyID;
        });
        subscriptions[i].WarrantyDescription = warranty?warranty.CoverageTerm:"";
      }

      return [0, {
        response: {
          message: subscriptions
        },
      }];
    ```
  - Set output as List and Item Type as Object as shown in the above diagram.

    With this we have implemented Get Collection to get the list of warranty subscriptions. Now let us implement Create Warranty Subscription to create some records before testing it.

### Implement Create (Post) Warranty Subscription.

1. Go to CREATE RECORD and configure the flow as below
  <br>![](/exercises/ex1/images/01_14_18_CreateFlow.png)

2. Set table field values from the request-payload
  <br>![](/exercises/ex1/images/01_14_19_ExtractPayload.png)
  <br>![](/exercises/ex1/images/01_14_20_ExtractPayLoad.png)
  <br>![](/exercises/ex1/images/01_14_21_ExtractPayload.png)

3. Configure all other fields and Save
  <br>![](/exercises/ex1/images/01_14_22_ExtractPayload.png) 

4. Set 'Send Successful Response" block
  <br>![](/exercises/ex1/images/01_14_23_SetResponseBlock.png) 

4. Save the project 

5. Restart the app and test
   - As earlier go back to DEPLOYMENT and click RESTART
   - To test we need to use some tools that can post the data. In this demo we will use [Postman](https://www.postman.com/downloads/).
   - Run 'GET warranties' end point to get some valid warranty-ids. This will be used to create warranty-subscriptions.
   - Run  'POST warrantysubscriptions' end point and provide following payload
   ```json
    {
      "Product": "1001",
      "IsActive": true,
      "AccountID": "10002",
      "WarrantyID": "<replace with an warranty-id in the previous step>",
      "WarrantyEnd": "2021-11-16"
    }
   ```
    <br>![](/exercises/ex1/images/01_14_24_TestPost.png)  
  - Test 'GET warrantysubscription' end point by repacing POST with GET action in the URL bar. 
## Summary

In this section we have created three backend service APIs that will be used to build the user interface in the next section. We have built APIs based on the local storage as well as created warapper API by consuming an external API (C4C Registered Product). 

Continue to - [Exercise 2 - Exercise 2 Description](../ex2/README.md)

