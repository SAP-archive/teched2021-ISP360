# Exercise 2 - Building the UI with the SAP AppGyver Composer

In this exercise, we will create the web application (UI) to list and create warranty subscriptions.

## Exercise 2.1 Create Frontend Project

After completing these steps you will have created and initialised an empty UI project to perform next set of exercises. You have also setup some parameters that we'll use later.

1. Save the backend project and click EXIT BACKEND button.

  <br>![](/exercises/ex2/images/02_21_00a_Exit.png)

 - Click APPS button to go to **SAP AppGyver Composer**:

  <br>![](/exercises/ex2/images/02_21_00b_Apps.png)

  - If you've taken a longer break you can log back in with your workshop user credentials (email/password):
  - https://platform.testgyver.com/auth/legacy

2. Create project by clicking CREATE NEW button and assign a name:

  <br>![](/exercises/ex2/images/02_21_01_CreateProject.png)
  <br>![](/exercises/ex2/images/02_21_02_CreateProject.png)

3. Rename the Empty Page and set the screen size

  - Here we can select the page size based on the target preferred device for which we area creating the application. We will use Web:

  <br>![](/exercises/ex2/images/02_21_03_RenameFirstPage.png)

4. Remove navigation

  - Project was created with a navigation to allow users to move between pages
  - We won't need the navigation for our two page application
  - Choose 'Navigation' from top (1) and check that 'Navigation header bar' (2) is not enabled by selecting 'No' (3)

  <br>![](/exercises/ex2/images/02_21_04_DisableNavigation.png)

  - Click 'Navigation menu' (1) and check that it is not enabled (2) and that our new WarrantySubscription page is selected 'Page' (3)

  <br>![](/exercises/ex2/images/02_21_05_DisableNavigation.png)

5. Close navigation view and click the toggle between View and Variables to navigate to variable editing view

  <br>![](/exercises/ex2/images/02_21_06_CloseNavigation.png)

  - Click 'Page Parameters' from left side (1)
  - These parameters are passed on to page when it is first opened
  - Click 'Add Parameter' (2)
  - Type 'AccountID' as parameter name (3) and give it some sensible default value. Keep parameter type as Text

  <br>![](/exercises/ex2/images/02_21_07_AddPageParam.png)

6. Save the project from top right corner - it is good practice ro save the project time to time

## Exercise 2.2 Create Data Sources

Now before proceeding to implement the UI, we need a way to fetch and create data using the API that we have implemented in the Exercise 1. This is done by creating data sources in the UI project. Note that we had also created Data Sources in the backend to implement the API but now we create the data sources in the UI project to use those APIs to read and create data.

1. Create Warranty Subscription Data Source

  - Switch to the 'Data' tab and click 'Add Data Source':
  - Select "AppGyver Cloud Integration (beta)":

  <br>![](/exercises/ex2/images/02_22_01_CreateDataSource.png)

  - Choose the Cloud Integration you just finished and WarrantySubscriptions:

  <br>![](/exercises/ex2/images/02_22_02_CreateDataSource.png)

2. Create 'Registered Product Party Information Collection' and 'Warranties' data sources in the same way.

  - Finally there Data Sources tab will look as following and you can close the Data view
  <br>![](/exercises/ex2/images/02_22_09_DataSourceSummary.png)

3. Save the project

## Exercise 2.3 Implement Warranty Subscription List Page

In this exercise we will create components to the list view to show all Warranty Subscriptions for given account. We will use new **SAP AppGyver** components that fetch data from our new backend with given conditions.

1. Clean-up and rename existing Components:

  - Choose the title (1) and change 'Content' from 'Properties' (2)
  - Type `Warranty Subscriptions`

  <br>![](/exercises/ex2/images/02_23_02_CreateLayout.png)

  - Remove paragraph and open Component Market

  <br>![](/exercises/ex2/images/02_23_03_RemoveP.png)

2. Install new component from the Component Market

  - Use this token to search for the component: `SfVOJZmYHpEB8vObtgisbg`
  - These Components will be released later without having to install them via tokens

  <br>![](/exercises/ex2/images/02_23_04_SfVOJZmYHpEB8vObtgisbg.png)

  - Choose Component from search results

  <br>![](/exercises/ex2/images/02_23_05_BasicDataTable.png)

  - Install Component and accept additional installs
  - Don't worry, it's not installing anything on you computer! It is only adding dependencies to the Composer project

  <br>![](/exercises/ex2/images/02_23_06_BasicDataTableAlert.png)

4. Drag 'Basic data table' component from components to canvas (1) and click 'Configure' button (2)

  <br>![](/exercises/ex2/images/02_23_07_DragBasicDataTable.png)

5. Choose Data Resource for the Table

  - Click value bind button:

  <br>![](/exercises/ex2/images/02_23_08_DataTableSource.png)

  - Choose 'Data resource':

  <br>![](/exercises/ex2/images/02_23_09_DataTableSource.png)

  - Choose 'WarrantySubscriptions':

  <br>![](/exercises/ex2/images/02_23_10_DataTableSource.png)

  - Click SAVE

  <br>![](/exercises/ex2/images/02_23_11_DataTableSource.png)

6. Now we can choose how to filter data from our backend to the table

  - Add condition (1)
  - Type 'AccountID' to property name (2)
  - Click value bind button (3)

  <br>![](/exercises/ex2/images/02_23_12_ConditionsAndColumns.png)

  - Choose 'Formula'

  <br>![](/exercises/ex2/images/02_23_13_ConditionsAndColumns.png)

  - Click existing formula to edit it
  <br>![](/exercises/ex2/images/02_23_14_ConditionsAndColumns.png)

  - Remove existing empty Formula
  - Either type the simple Formula in or use UI to guide you through it
  - Click SAVE button to go back to Table configuration

  <br>![](/exercises/ex2/images/02_23_15_ConditionsAndColumns.png)

7. Hide all other fields than Product, CoverageTerm and WarrantyEnd. You can organize fields ordering by dragging them with a drag handle. Display text allows you to control what is shown to users as column header.

  <br>![](/exercises/ex2/images/02_23_16_Columns.png)

8. Save and launch the application in the preview portal. Once the application is launched you should see list of warranty subscriptions created.

  <br>![](/exercises/ex2/images/02_26_01_OpenPreview.png)

  - Click OPEN APP IN PREVIEW PORTAL button

  <br>![](/exercises/ex2/images/02_26_02_OpenInPreviewPortal.png)

  - Open your App

  <br>![](/exercises/ex2/images/02_26_03_PreviewPortal.png)

   - You will see a note 'No Data Available'
   - Add query string parameter `?AccountID=1000034` to the end of the URL¨
   - Ie. `https://platform.preview.testgyver.com/<your app id>/productwarranty/page.Page1?AccountID=1000034`

  <br>![](/exercises/ex2/images/02_23_17_Safari.png)

## Exercise 2.4 Implement Warranty Subscription Creation Page
In this section we will create a page using which a warranty subscription can be created. This will be launched from first page using '+' button.

1. Open PAGES view (1) and create a new page (2)

  <br>![](/exercises/ex2/images/02_24_01_CreateNewPage.png)

  - Name it `Warranty Subscription Creation`

  <br>![](/exercises/ex2/images/02_24_02_CreateNewPage.png)

2. Switch variable editing view (1) to add page parameter (2, 3) we get from list view

  - Type `AccountID` to Parameter name (4)

  <br>![](/exercises/ex2/images/02_24_03_PageParam.png)

3. While in variable editing view add data variables to components we're about to create
  - Choose 'Data Variables' (1)
  - Add Data Variable (2)
  - Choose 'RegisteredProductPartyInformationCollection' but rename it to be shorter (3)
  - Make sure Data variable type is Collection
  - Add Filter condition (4)

  <br>![](/exercises/ex2/images/02_22_10_DataVariables.png)

  - Choose 'Object with properties'

  <br>![](/exercises/ex2/images/02_22_11_DataVariablesConditions.png)

  - Click 'Add Condition' button

  <br>![](/exercises/ex2/images/02_22_12_DataVariablesConditions.png)

  - Choose 'RoleCode' and expect it to equal 60
  - Then create another condition for 'PartyID' and click value bind button:

  <br>![](/exercises/ex2/images/02_22_13_DataVariablesConditions.png)

  - Choose 'Data & Variables':

  <br>![](/exercises/ex2/images/02_22_14_DataVariablesConditions.png)

  - Choose 'Page parameter':

  <br>![](/exercises/ex2/images/02_22_15_DataVariablesConditions.png)

  - Choose 'AccountID' and the final conditions are done:

  <br>![](/exercises/ex2/images/02_22_16_DataVariablesConditions.png)

4. Add another Data variable from Warranties but this time no conditions are needed

  <br>![](/exercises/ex2/images/02_22_17_WarrantiesDataVariable.png)

5. Open Logic Editor from the bottom of the screen and remove delay from both Data Variables

  <br>![](/exercises/ex2/images/02_24_04_LogicEditor.png)

  - Delay is useful if you need to keep App up to date with latest changes from the backend but in this exercise we don't need that so it's better to remove it

  <br>![](/exercises/ex2/images/02_22_18_RemoveDelay.png)

6. Add three 'Page variables' to hold the data selected by the user:

| Name | Type |
|------|------|
| selectedDate | date text |
| selectedProduct | text |
| selectedWarranty | text |

  - Click 'Page Variables' (2)
  - Add page variable (3)
  - Make sure the types are correct! Especially for `selectedDate` (5)

  <br>![](/exercises/ex2/images/02_24_07_AddPageVariables.png)

7. Go back to View and create Required Controls on the Page:

  - Set the Title as `Warranty Subscription Creation`
  - Frag two dropdowns from left side to canvas
  - Rename the dropdowns to `Registered Products` and `Warranty Terms` from right side Properties like we've done earlier in this workshop

  <br>![](/exercises/ex2/images/02_24_03_CreateLayout.png)

8. Create Date picker control for Warranty End date

  - Install new component from Component Market same way we did it in last step
  - Use token `Ft6B2OsfRl-Woh0brYzOMw` to search a component and install it
  - Drag new Component to canvas
  - Click value bind button from right side 'Properties' and you'll see familiar modals appear:

  <br>![](/exercises/ex2/images/02_24_04a_AddDataPickerComponent.png)

  - Choose 'Data & Variables', 'Page Variables' and bind Value to `selectedDate`
  - Type `Warranty End` to Components 'Label'

  <br>![](/exercises/ex2/images/02_24_04b_DatePickerConfig.png)

9. Create Save and Cancel buttons

  - First create a container to hold and align the buttons

  <br>![](/exercises/ex2/images/02_24_04c_CreateActionContainer.png)

  - Then drag buttons inside the container

  <br>![](/exercises/ex2/images/02_24_05a_CreateButtons.png)

  - Change buttons styles accordingly

  <br>![](/exercises/ex2/images/02_24_05b_CreateButtons.png)

  - Go to Layout tab and open 'Width and Height' section to change button width to 'Fit content':

  <br>![](/exercises/ex2/images/02_24_06_ButtonWidth.png)

  - Change button 'Labels' to `Cancel` and `Create`:

  <br>![](/exercises/ex2/images/02_24_05c_CreateButtons.png)

10. Set 'Option list' and 'Selected value' for the Registered products dropdown:

  - Click on the 'Option list' and set the formula value to:
  ```
  MAP<Product>(data["Registered Products"], { label: Product.RegisteredProductID, value: Product.RegisteredProductID })
  ```
  - In this formula, we are transforming the data retrive from the backend to the format that Option list needs
  - Set the 'Selected value' to the page variable `selectedProduct` that we have created earlier. By doing this we will get the registered product selected by the user

  <br>![](/exercises/ex2/images/02_24_08_SetOptionList.png)

11. Set 'Option list' and 'Selected value' for the Warranty dropdown:

  - Click on the 'Option list' and set the formula value to:

  ```
  MAP<Warranty>(data["Warranties1"], { label: Warranty.CoverageTerm, value: Warranty.id})
  ```

  - Set the 'Selected value' to the page variable `selectedWarranty`

  <br>![](/exercises/ex2/images/02_24_09_SetOptionList.png)

12. Configure Create logic

  - Select the 'Create' button (1) and click on the 'Show Logic for Button1' from the bottom of the page (2)

  <br>![](/exercises/ex2/images/02_24_10_CreateButtonLogicEditor.png)

  - Drag 'Create Record' from 'Data' section (1)
  - Set 'Resource Name' to 'WarrantySubscriptions' (2)
  - Click 'Custom object' from 'Record' property (3)

  <br>![](/exercises/ex2/images/02_24_11_CreateRecord.png)

  - Bind values from 'Page Variables' and 'Page Parameters'
  - Leave `identifier` and `CoverageTerm` empty

  <br>![](/exercises/ex2/images/02_24_12_ButtonPayload.png)

  - Drag 'Open page' node from left side to Canvas (1)
  - Connect nodes together (2, 3)
  - Set navigation back to the 'Warranty Subscription' list page (4) and bind 'AccountID' to 'Page Parameter' with same name (5)

  <br>![](/exercises/ex2/images/02_24_13_NavigateToListAfterSuccess.png)

13. Also configure Cancel button to navigate back to the list page (same way as above).

## Exercise 2.5 Link to Creation page from the List page

In this section we create the '+' button and link it to open the Warranty Subscription Creation page.

1. Save the project and go to 'Warranty Subscription' page

  <br>![](/exercises/ex2/images/02_25_01_GoToPage1.png)

2. Drag Icon component to canvas above table and choose icon for the component

  <br>![](/exercises/ex2/images/02_25_02_DragIcon.png)
  <br>![](/exercises/ex2/images/02_25_03_ChooseIcon.png)

3. Set Icon layout to be at the right side of the screen

  <br>![](/exercises/ex2/images/02_25_04_IconLayout.png)

4. Open Icon logic editor from the dark bar at the bottom of the page

  - Drag 'Open page' node to canvas and connect 'Component tap' to it
  - Make sure 'Page' is selected as 'Warranty Subscriptions Creation'
  - Map `AccountID` to 'Data and Variables', 'Page Parameter' and choose 'AccountID'

  <br>![](/exercises/ex2/images/02_25_05_IconLogic.png)

## Exercise 2.6 Build and distribution

Finally we can build and distribute our project. Preview Portal URL that we used earlier cannot be shared with friends or colleagues because it has been authenticated one-time for your browser. That's why that same URL cannot be used to embed the page to your **SAP Sales and Service Cloud** mashups. Preview is a tool during the design and development. Now we're about to build the App for distribution.

1. Save and click 'Launch' from the top:

  <br>![](/exercises/ex2/images/02_26_01_OpenPreview.png)

2. Click 'Distribute' from left side and then 'Open Build Service':

  <br>![](/exercises/ex2/images/02_26_04_StartBuild.png)

  - Click CONFIGURE button

  <br>![](/exercises/ex2/images/02_26_04_Build.png)

  - In the below step you will give the unique name that will make the final url

  <br>![](/exercises/ex2/images/02_26_05_Build.png)

  - Continue with the 'Save & Next' with default values:

  <br>![](/exercises/ex2/images/02_26_06_Build.png)

  - Continue with the 'Save & Next' with default values:

  <br>![](/exercises/ex2/images/02_26_07_Build.png)

  - Continue with the 'Save & Next' with default values:

  <br>![](/exercises/ex2/images/02_26_08_Build.png)

  - Go back to **SAP Appgyver** and click on the build step

  <br>![](/exercises/ex2/images/02_26_09_Build.png)

  - Select a runtime version (preferably latest one) and provide the version number `1.0.0`
  - Copy the domain name but don't try to reach it yet, it will only work after the build has been 'Delivered'
  - The build may take some time to complete

  <br>![](/exercises/ex2/images/02_26_10_Build.png)

## Summary

You've now implemented the frontend application and got the final url that will be used to mashup the application inside C4C.

The application url will look like this:
`http://<unique name given>.wsapps.testgyver.com/?AccountID=1000000`. It accepts one query parameter called `AccountID`.

Continue to - [Exercise 3 - Excercise 3 ](../ex3/README.md)
