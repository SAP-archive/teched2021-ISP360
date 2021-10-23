# Exercise 2 - Exercise 2 Description

In this exercise, we will create the web application(UI) to list and create warranty subscriptions.

## Exercise 2.1 Create Frontend Project

After completing these steps you will have created and empty project.

1. Login to the AppGyver Composer with selected user credentials (email/password):
  - https://testgyver-qa-platform.testgyver.com/auth/legacy 

2. Create project by clicking Create New button and assign a name:
  <br>![](/exercises/ex2/images/02_21_01_CreateProject.png)
  <br>![](/exercises/ex2/images/02_21_02_CreateProject.png)

3.	Rename the Empty Page and set screen size:
   Here we can select the page size based on the target preferred device for which we area creating the application. We will use Web.
  <br>![](/exercises/ex2/images/02_21_03_RenameFirstPage.png)

4. Set navigation title: When the project created, the Empty Page was aslo marked as default navigation page. Since we have chnage the title we will also adjust the navigation tab title.
  <br>![](/exercises/ex2/images/02_21_04_SetNavigationTitle.png)

## Exercise 2.2 Create Data Sources
Now before proceeding to implement UI, we need a way to fetch and create data using the API that we implemented in the execise 1. This is done by creating data sources in the UI project. Note we have also created Data Sources in the backend to implement the API but now we create in the UI project that refer to those APIs.

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

  - Move to TEST tab, provide accound id value and RUN TEST. If the result is displayed, click SET SCHEMA FROM RESPONSE.
  <br>![](/exercises/ex2/images/02_22_05_CreateDSTest.png) 

  - Adjust the schea sligtly: Byt default it generates some fields as 'integer' (based on value), convert them to 'text'.
  <br>![](/exercises/ex2/images/02_22_06_CreateDSSchema.png) 

2. Move to 'CREATE RECORD' (for Warraty Subscription Data Source) and set the method 'Enabled' and set the schema to 'Use Get Schema'.

3. Create 'Registered Products' and 'Warranties' data sources in the same way.        
  However for these data sources:
  - We don't need CREATE RECORD to be enabled. 
  - Also AccountID parameter to registered products data source
  - Finally there Data Sources tab will look as following:
  <br>![](/exercises/ex2/images/02_22_09_DataSourceSummary.png) 
  
## Exercise 2.3 Implement Warrant Subscription List Page

1. Switch to Warranty Subscription page:
  <br>![](/exercises/ex2/images/02_23_01_SwitchToPage.png) 

2. Create Layout as below
  Note that we need a container to host actions like 'create record'. The to create a table, we have a 'scroll container' to support scrolling and two 'row' layouts - one for the table header and other for data rows.
  <br>![](/exercises/ex2/images/02_23_02_CreateLayout.png) 

3. Add plus icon & its alignment
  Here we configure a 'action icon' that will be used to add a new warranty. Currently we just add the icon and come back latter to attach the navigation.
  <br>![](/exercises/ex2/images/02_23_03_SetPlusIcon.png)   
   Select the container layout and set the alignment to horizontal and right alignment.
  <br>![](/exercises/ex2/images/02_23_04_SetActionbarAlignment.png) 

4. Set Table Columns
  By default a row-layout contains two columns. First let us add one more column:
  <br>![](/exercises/ex2/images/02_23_05_AddCell.png)  

  Drag-n-drop 'title' controls in each column and set the text as below:  
  <br>![](/exercises/ex2/images/02_23_06_SetHeaderCells.png) 

5. Configure data row:
  - Earlier we created data sources to read data from the backend. Now we need to created a data-variable to actually read and include the data in this page.
  <br>![](/exercises/ex2/images/02_23_07_AddDataVariables.png)  
  
  - Now again switch to the VIEW and add one more cell to the second Row layout:  
  <br>![](/exercises/ex2/images/02_23_08_AddCellToDataRow.png)  

  - Bind the row to data:
  <br>![](/exercises/ex2/images/02_23_09_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_10_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_11_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_12_BindDataVariable.png)  
  <br>![](/exercises/ex2/images/02_23_13_BindDataVariable.png)  

 - Bind the cell to respective data-field:
  <br>![](/exercises/ex2/images/02_23_14_ConfigureCellTitle.png)  
  <br>![](/exercises/ex2/images/02_23_15_ConfigureCellTitle.png)  
  <br>![](/exercises/ex2/images/02_23_16_ConfigureCellTitle.png) 
  <br>![](/exercises/ex2/images/02_23_17_ConfigureCellTitle.png)  
  <br>![](/exercises/ex2/images/02_23_18_ConfigureCellTitle.png) 

- Launch the application to test Warranty Subscription list screen
  Save the application and test in the Preview portal:
  <br>![](/exercises/ex2/images/02_23_19_Launch.png) 
  <br>![](/exercises/ex2/images/02_23_20_Launch.png) 

## Exercise 2.4 Implement Warrant Subscription Creation Page

## Summary

You've now ...

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
