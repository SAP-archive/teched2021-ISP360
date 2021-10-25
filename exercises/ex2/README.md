# Exercise 2 - Building the UI with the AppGyver Composer

In this exercise, we will create the web application(UI) to list and create warranty subscriptions.

## Exercise 2.1 Create Frontend Project

After completing these steps you will have created and initialised an empty UI project to perform next set of execises.

1. Login to the AppGyver Composer with selected user credentials (email/password):
  - https://testgyver-qa-platform.testgyver.com/auth/legacy 

2. Create project by clicking CREATE NEW button and assign a name:
  <br>![](/exercises/ex2/images/02_21_01_CreateProject.png)
  <br>![](/exercises/ex2/images/02_21_02_CreateProject.png)

3. Rename the Empty Page and set the screen size:
   Here we can select the page size based on the target preferred device for which we area creating the application. We will use Web.
  <br>![](/exercises/ex2/images/02_21_03_RenameFirstPage.png)

4. Set the navigation title: When the project was created, the Empty Page was aslo marked as default navigation page. Since we have chnaged the title we will also adjust the navigation tab title.
  <br>![](/exercises/ex2/images/02_21_04_SetNavigationTitle.png)

## Exercise 2.2 Create Data Sources
Now before proceeding to implement the UI, we need a way to fetch and create data using the API that we have implemented in the execise 1. This is done by creating data sources in the UI project. Note that we had also created Data Sources in the backend to implement the API but now we create the data sources in the UI project to use those APIs to retrive/create data.

1. Create Warranty Subscription Data Source
  - Swicth to the 'Data' tab and click 'Add Data Source':
  <br>![](/exercises/ex2/images/02_22_01_CreateDataSource.png)  
  - Select REST API direct integration:

  <br>![](/exercises/ex2/images/02_22_02_CreateDataSource.png)  
  - Enter the details as below:

  Note in the Resource URL, copy the URL for Warranty Subscription API created in the exercise 1.  
  <br>![](/exercises/ex2/images/02_22_03_CreateDataSource.png)  

  -  Switch to GET COLLECTION and add 'AccountID' as below:
  <br>![](/exercises/ex2/images/02_22_04_CreateDSParameter.png)   

  - Move to the TEST tab, provide accound id value and RUN TEST. If the result is displayed, click on SET SCHEMA FROM RESPONSE.
  <br>![](/exercises/ex2/images/02_22_05_CreateDSTest.png) 

  - Adjust the schema sligtly: By default it generates some fields as 'integer text'. This is because the sample value returned from the APIs were integer. However, the actual types of these fields are 'text'. So, we set them to 'Text' manually. 
  <br>![](/exercises/ex2/images/02_22_06_CreateDSSchema.png) 

2. Move to 'CREATE RECORD' (for Warraty Subscription Data Source) and set the method 'Enabled' and set the schema to 'Use Get Schema'.
  <br>![](/exercises/ex2/images/02_22_06a_CreateDSPost.png) 

3. Create 'Registered Products' and 'Warranties' data sources in the same way.        
  However for these data sources:
  - We don't need CREATE RECORD to be enabled. 
  - Also add AccountID parameter to registered products data source.
  - Don't forget to run the test for the collection and set schema from response.
  - Finally there Data Sources tab will look as following:
  - Save the project - it is good practice ro save the project time to time.
  <br>![](/exercises/ex2/images/02_22_09_DataSourceSummary.png) 
  
## Exercise 2.3 Implement Warrant Subscription List Page

1. Switch to Warranty Subscription page:
  <br>![](/exercises/ex2/images/02_23_01_SwitchToPage.png) 

2. Create Layout as below
  Note that we need a container to host actions like 'add new'. Then to create a table, we have a 'scroll container' to support scrolling and two 'row' layouts - one for the table header and the other for data rows.
  <br>![](/exercises/ex2/images/02_23_02_CreateLayout.png) 

3. Add plus icon & adjust alignment
  Here we configure a 'action icon' that will be used to add a new warranty. Currently we just add the icon and come back latter to attach the navigation.
  <br>![](/exercises/ex2/images/02_23_03_SetPlusIcon.png) 
  
  Select the container layout and set the alignment to horizontal and right alignment.
  <br>![](/exercises/ex2/images/02_23_04_SetActionbarAlignment.png) 

4. Set Table Columns
  By default a row-layout contains two columns. First let us add one more column:
  <br>![](/exercises/ex2/images/02_23_05_AddCell.png)  

  Drag-n-drop 'title' controls in each column and set the text as below. Adjust the font size to desired size: 
  <br>![](/exercises/ex2/images/02_23_06_SetHeaderCells.png) 

5. Configure data row:
  - Note that our AppGyver application will be finally hosted inside a C4C screen. It will take a paramneter `AccountID` from the host screen and filter the wareranty subscriptions and registered products based on that. So, we need to define a page parameter `AccoundID` and also a App variable to store this `AccoundID` which is shared across the screens.
 <br>![](/exercises/ex2/images/02_23_06a_AddPageParameter.png) 
 <br>![](/exercises/ex2/images/02_23_06b_AddAppVariable.png) 
   
  - Earlier we created data sources to read data from the backend. Now we need to created a data-variable to actually read and include the data in this page.
  <br>![](/exercises/ex2/images/02_23_07_AddDataVariables.png)  
  
  - Now again switch to the VIEW and add one more cell to the second Row layout (the data row layout):  
  <br>![](/exercises/ex2/images/02_23_08_AddCellToDataRow.png)  

  - Bind the row to data variable `WarrantyDescription`. This will result in one table row created for every raecord in the data variable. 
  <br>![](/exercises/ex2/images/02_23_09_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_10_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_12_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_13_BindDataVariable.png)  

 - Bind the cell to respective data-field:
  <br>![](/exercises/ex2/images/02_23_14_ConfigureCellTitle.png)  
  <br>![](/exercises/ex2/images/02_23_15_ConfigureCellTitle.png)  
  <br>![](/exercises/ex2/images/02_23_16_ConfigureCellTitle.png) 
  <br>![](/exercises/ex2/images/02_23_17_ConfigureCellTitle.png)  
  <br>![](/exercises/ex2/images/02_23_18_ConfigureCellTitle.png) 

6. Assign App variable `AccoundID` to the `AccoundID` page paremter. Note that earlier we have created the App variable but we have not assigned it a value yet. Let assign it.
  - Open the 'Logic' panel if this is not opened already
  <br>![](/exercises/ex2/images/02_23_18a_AssignAppVariable.png) 

  - Set the AccountID app variable to the AccountID page parameter
  <br>![](/exercises/ex2/images/02_23_18b_AssignAppVariable.png) 

7. Launch the application to test Warranty Subscription list screen
  Save the application and test in the Preview portal:
  <br>![](/exercises/ex2/images/02_23_19_Launch.png) 
  <br>![](/exercises/ex2/images/02_23_20_Launch.png) 

## Exercise 2.4 Implement Warrant Subscription Creation Page
In this section we will create a page using which a warranty subscription can be created. This will be launched from first page using '+' button.

1. Create New Page and name it 'Create Warranty Subscription'
  <br>![](/exercises/ex2/images/02_24_01_CreateNewPage.png) 
  <br>![](/exercises/ex2/images/02_24_02_CreateNewPage.png)  

2. Create Required Controls on the Page:
  - Set the Title as 'Warranty Subscription Creation' 
  - Create two dropdowns to select 'Registered Product' and 'Warranty Terms'
  <br>![](/exercises/ex2/images/02_24_03_CreateLayout.png)  

3. Create Save and Cancel buttons
  - First create a container to hold and align the buttons
  <br>![](/exercises/ex2/images/02_24_04_CreateActionContainer.png)  

  - The create the buttons inside the container:
  <br>![](/exercises/ex2/images/02_24_05_CreateButtons.png) 

4. Switch to the VARIABLES view and add data variables to fetch registered products using the registered product data source. Set the `AccountID` parameter to the formula: `"'" + appVars.AccountID + "'"`. 
  <br>![](/exercises/ex2/images/02_24_06_AddDataVariables.png) 
  <br>![](/exercises/ex2/images/02_24_06a_AddDataVariables.png) 
  <br>![](/exercises/ex2/images/02_24_06b_AddDataVariables.png) 
  <br>![](/exercises/ex2/images/02_24_06c_AddDataVariables.png) 

5. Similarly add a data variable for 'warranties' data source. Note that there is no parameter defined for the warranties data source.

6. Add some 'page' variables to hold the data selected by the user:
  - selectedDate : type `date text`
  - selectedProduct: type `text`
  - selectedWarranty: type `text`
  <br>![](/exercises/ex2/images/02_24_06_AddDataVariables.png) 

4. Set 'Option list' for the registered products
  - Click on the 'Option list' and set the formula value to:
  `MAP(data.RegisteredProducts1, {label: item.RegisteredProductID, value:item.RegisteredProductID})`.
  In this formula, we are transforming the data retrive from the backend to the format that Option list needed.
  <br>![](/exercises/ex2/images/02_24_08_SetOptionList.png) 
  <br>![](/exercises/ex2/images/02_24_09_SetOptionList.png) 
  <br>![](/exercises/ex2/images/02_24_10_SetOptionList.png) 

5. Set the 'Selected value' to the page varibale `selectedProduct` that we have created earlier. By doing this we will get the registered product selected by the user.
  <br>![](/exercises/ex2/images/02_24_11_SetSelectedValue.png)  

6. Similarly configure the 'Warranty Terms' drop down:
  - Option list: Set the value to formula `MAP(data.Warranties1, {label:item.CoverageTerm,value:item.id})` 
  - Selected value: To page variable `selectedWarranty`
  <br>![](/exercises/ex2/images/02_24_12_ConfigureWarrantyDropDown.png)

7. Configure End Date Input
  - Bind the value property to the page variable: `selectedDate`
  - Set the place holder text to 'YYYY-MM-DD'
  <br>![](/exercises/ex2/images/02_24_13_ConfigureEndDate.png) 

8. Configure Save logic
  - Select the 'Save' button and click on the 'Show Logic for Button1'
  <br>![](/exercises/ex2/images/02_24_14_SaveLogic.png) 

  - Drag-n-drop 'Crete Record' from the left panel and configure as below:
  <br>![](/exercises/ex2/images/02_24_15_SaveLogic.png) 
  <br>![](/exercises/ex2/images/02_24_16_SaveLogic.png) 

  - Set navigation back to the 'Warranty Sybscription' list page
  <br>![](/exercises/ex2/images/02_24_17_NavigateToList.png) 

9. Also configure Cancle button to navigate back to the list page (same way as above).

10. Save and launch the application in the preview portal. Once the application is laucnhed you should see list of warranty subscriptions created. Add the'+' button on top-right corner to add new warranty subscription:
  <br>![](/exercises/ex2/images/02_24_18_SaveAndLaunch.png) 
  <br>![](/exercises/ex2/images/02_24_19_SaveAndLaunch.png) 

11. Get the distributable URL
  Till now we have tested inside preview portal. Now we get the final URL by deploying it. 
  <br>![](/exercises/ex2/images/02_24_20_GetURL.png) 
  <br>![](/exercises/ex2/images/02_24_20_GetURL.png) 
  
  - In the below step you will give the unique name that will make the final url. 
  <br>![](/exercises/ex2/images/02_24_20_GetURL.png)     
  
## Summary

You've now implemented the UI appliction and got the final url that will be used to mashup the application inside C4C.

The application url will look like this:
`http://<unique name given>.wsapps.testgyver.com/?AccountID=1000000`. It accepets one query parameter called `AccountID`.

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
