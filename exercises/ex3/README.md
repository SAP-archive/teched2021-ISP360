# Exercise 3 - Emebedding the Web Application in C4C

In this exercise, we will will embed the webapp that was created in the previous step inside the Account Detail screen of C4C. This exercise consists of mainly two parts:
- Creating a mashup configuration that stores information about the webapp like url and parameters.
- Emebedding the mashup object into the Agent Desk application.  

## Exercise 3.1 Create a Mashup object in the C4C

In this section we will create a mashup object using the webapp url that we have created in the excecise 2.  

1. Login to the C4C and navigate to the Mashup Authoring screen
  - Create an HTML mashup as shown below:
 <br>![](/exercises/ex3/images/03_01_01_CreateMashup.png)

2. Configure the mashup
  - Select `With port binding` and Port binding : `Additional Account Information`
  - Give the mashup some name like `Warranties` 
  - Scroll down and configure url and parameters binding as in the next diagram
  - Test using `Preview` 
 <br>![](/exercises/ex3/images/03_01_02_CreateMashup.png)
 <br>![](/exercises/ex3/images/03_01_03_CreateMashup.png)

## Exercise 3.2 Configure Agent Desktop application
 
In this section we will configure the Account Detail screen to use the above mashup object.

1. Open Account Object Work List, search for the `Bank Tech` account and open it as below:
 <br>![](/exercises/ex3/images/03_02_01_OpenAccounts.png)

2. In the opened screen, start `Adaptation Mode`
 <br>![](/exercises/ex3/images/03_02_02_StartAdaptationMode.png)

3. Add a tab to host the mashup inside Account Detail screen:
 <br>![](/exercises/ex3/images/03_02_03_AddTab.png)
 <br>![](/exercises/ex3/images/03_02_04_AddTab2.png)

4. Add mashup as below:
  - Select the Tab that you just added
  - Select the `Pencil icon` in the default section as below 
  - In the right hand side car, nagivate to the `View` using the back button 
  - Click Add Mashup
 <br>![](/exercises/ex3/images/03_02_05_AddMashup.png)
  
  - In the opened popup, search for the mashup that you created earlier 
  - Make sure to set full width, hide the header and set height to cover full area in the tab.
 <br>![](/exercises/ex3/images/03_02_06_AddMashup2.png)

5. Hide extra section that was added by default:
 <br>![](/exercises/ex3/images/03_02_07_HideExtraSection.png) 

6. End Adaptation Mode:
 <br>![](/exercises/ex3/images/03_02_08_EndAdaptationMode.png) 

7. Test the embedded mashup:
 <br>![](/exercises/ex3/images/03_02_09_TestApplication.png) 
## Summary
 With this we have completed all the execises in this workshop. Thanks a lot for following this up. 
