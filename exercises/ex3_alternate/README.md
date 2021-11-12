# Exercise 3 - Emebedding the Web Application in C4C

In this exercise, we will will embed the webapp that was created in the previous step inside the Agent Desk application of C4C. This exercise consist of mainly two parts:
- Creating a mashup configuration that stores information about the webapp like url and parameters.
- Emebedding the mashup object into the Agent Desk application.  

## Exercise 3.1 Create a Mashup object in the C4C

In this section we will create a mashup object using the webapp url that we have created in the excecise 2.  

1. Login to the C4C and navigate to the Mashup Authoring screen
  - Create an HTML mashup as shown below:
 <br>![](/exercises/ex3/images/03_01_01_CreateMashup.png)

2. Configure the mashup
  - Select `With port binding` and Port binding : `Agent Desk Information`
  - Scroll down and configure url and parameters binding as in the next diagram
  - Test using `Preview` 
 <br>![](/exercises/ex3/images/03_01_02_CreateMashup.png)
 <br>![](/exercises/ex3/images/03_01_03_CreateMashup.png)

## Exercise 3.2 Configure Agent Desktop application
 
In this section we will configure the Agent Desk application to use the above mashup object.

1. Open Agent Desk configuration screen
 <br>![](/exercises/ex3/images/03_02_01_ConfigAgentDesktop.png)

2. Go to `Additional Tab Settings` 
  In this screen you configure three things:
  - Create or Configure an existing Tab (currently there is a limit on number of tabs). For this you just select a row in the Tabs table and give a name: `Warrangies(Teched)` in the below example.
  - Select the mashup that we have created in the preview step to be shown in selected tab. `ISP360-sample` in the below example.
     - Also bind the mashup-parameter (`AccountID`) to a data field.
  - Configure the `Action Menu` through which this tab can be opened. `Show Warranties` in this case.
 <br>![](/exercises/ex3/images/03_02_02_EmbedMashup.png)

3. Open the Agent Desk App to see the `warraties app` embedded in the Agent Desk.
 <br>![](/exercises/ex3/images/03_02_03_RunTheApplication.png)
 <br>![](/exercises/ex3/images/03_02_03_RunTheApplication.png)
    
## Summary
 With this we have completed all the execises in this workshop. Thanks a lot for following this up. 
