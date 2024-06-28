<div class="draftWatermark"></div>

# Process Automation

---

In the previous exercise, we prepared the S/4 API to be used within a business process. In this exercise, we will design the business process to create a Business Partner.


![](vx_images/287066268879516.png)

The process will consist of:

- A request form
- A step to enrich the initial data
- An approval step to confirm data is correct
    - If approved: Business partner will be created in S/4, and a notification will be sent to the requestor
    - If declined: A mail notification to the requestor

## Create business process project

From the SAP [SAP Build Lobby](https://build02-worksop.eu10.build.cloud.sap/):

1. Create a new project:

    ![](vx_images/530197436949133.png )

2. Select _Build an Automated Process_:

    ![](vx_images/411047094795708.png )

3. Select _Business Process_:

    ![](vx_images/151377846785066.png )

4. Give the following name to the project and click _Create_:

    ```
    ${number} BTP creation process
    ```


![](vx_images/388516504754652.png )
    The project will be created. If the project does not open in a new tab, click on it once it appears in the Lobby:


![](vx_images/100350447335860.png )
> [!TIP|icon:fa-solid fa-check|label:Congratulations]
> You have successfully created a new project for a business process. 

## Create a process inside the project

The project editor will open:

![](vx_images/320310603094195.png )

> [!INFO]
> Projects are composed of different artifacts, you can read more about them in the documentation: [Business Process Projects](https://help.sap.com/docs/build-process-automation/sap-build-process-automation/business-process-projects?locale=en-US)
> 
> 

![](vx_images/43790973434833.png )
1. Add a new process. Give it the following name (the identifier will auto populate), and click _Create_:

    ```
    ${number} BP approval process
    ```

   
    
![](vx_images/364190328248912.png )
    
  
    

![](vx_images/537981513988762.png )
    The empty process will look like:

   

![](vx_images/371271580644621.png )
> [!TIP|icon:fa-solid fa-check|label:Congratulations]
> You have successfully created the main process of your project. 

## Create forms and approvals

Our process will include a request form, approval forms, and forms to notify about the status of the requests.

### Creation Form

To create the form that will start this process:

1. Click the ➕ button on the _Trigger_ box > _Form_ > _New Form_:

  
    ![](vx_images/592120490866013.gif )

2. Give a name to the form and click _Create_:

    ```
    Creation Form
    ```

  
    ![](vx_images/255020647096157.png )

3. Double-click on the newly created form:

    
    
![](vx_images/410790613047373.png )

    > [!NOTE]
    > The Form editor will open. Here, you can drag and drop the elements and set titles and labels

    
![](vx_images/3362559906967.gif )

4. Follow the instructions to add the following elements:
    - Headline 1:
        ```
        New Business Partner Application Form
        ```
    - Paragraph:
        ```
        Please provide all required details below to complete the formalities. You will be notified via email if you qualify for doing business with us. Thank you for your interest in our company.
        ```
    - Dropdown:
        ```
        Initials
        ```
        Add the following options under _Manual definition_:
        ```
        Mr.
        Ms.
        Mrs.
        ```
        ![](vx_images/260591683247383.png )
    - Text:
        ```
        First Name
        ```
  
        
![](vx_images/596100613732254.png )
    - Text:
        ```
        Last Name
        ```
    - Text: 
        ```
        Email
        ```
        Add the following regular expression as custom input validation:
        ```
        .+@.+\..+
        ```

       
        
![](vx_images/227321803297822.png )

        > [!ATTENTION]
        > Make sure there is no **new line** in the validation box.
        > 
     
   ![](vx_images/475472200832073.png )

    - Dropdown: 
        ```
        Category
        ```
        Add the following options under _Manual definition_:
        ```
        1
        2
        3
        ```
       
  ![](vx_images/230921762792502.png )
    - Text:
        ```
        Organization
        ```
    - Text:
        ```
        Search Term
        ```
    - Text Area:
        ```
        Additional Comment
        ```
       
        
![](vx_images/453851721887579.png )
    > [!NOTE]
    > All inputs should be marked as required except the last _Additional Comment_

5. Save the form


![](vx_images/82470837821039.png )
### Creation confirmation

The next form we will prepare is the creation confirmation. This form will appear after the Business Partner is created in S/4, and will notify the requestor. As before, we will leverage the forms we already have, to save us some time.

1. Go to the _Overview_ tab:

    ![](vx_images/311771300140339.png )

2. Find the creation form, open the menu on the side and click on _Duplicate_:

  
    ![](vx_images/491651265011015.png )

3. Give the form a new name and click _Duplicate_:

    ```
    Creation confirmation
    ```

   
    
![](vx_images/69262149493341.png )
4. Follow the instructions to add and edit the fields:

    Change the title and description:
    - Headline 1: 
        ```
        Business Partner Creation Confirmation
        ```
    - Paragraph:
        ```
        Thank you for showing interest in working with us. We are happy to inform you that we have accepted your proposal and you have been added as new business partner in our company with details below. Congratulations!
        ```

    Remove the following fields:

    - Initials
    - Email
    - Category
    - Search term
    - Additional comment

  

![](vx_images/464801169220489.png )
    Make the remaining fields _Read only_:

  
    
![](vx_images/66732320543242.png )
    Add new fields:

    - Text: make read-only
        ```
        Business partner number
        ``` 
    - Paragraph: 
        ```
        We would like to finalize the contract and have you begin work as soon as possible.

        Please verify the details above and press SUBMIT button to acknowledge the acceptance.
        ```

     
        
![](vx_images/232121387607401.png )
5. Save the form

The resulting form should look like:


![](vx_images/366032521187727.png )
### Approval form

I promise we are almost there. This will be the last form that you will build. The form will serve as an approval step to confirm all the information is correct before creating the business partner in the S/4 system.

1. Go to the _Overview_ tab:

  
    
![](vx_images/570281546294866.png )
2. Click on _Create_ > _Approval_:

   
   ![](vx_images/127222549641893.png )

3. Give it the following name, base the form on the _Creation form_ and click on _Create_:

    ```
    Business partner approval
    ```

 
    
![](vx_images/327131211046228.png )

4. The fields from the _Creation form_ will appear as read only, headings and paragraphs have been removed. Add the fields from the list below:

    At the begining of the form:
    - Modify the headline: 
        ```
        Approve new Business Partner request
        ```
    - Paragraph: 
        ```
        A new business partner request has been initiated with below details. We have verified the details to ensure that there is no inconsistencies with the existing business partners. Please approve or reject the request:
        ```

    At the end of the form:
    - Paragraph: 
        ```
        If you reject the proposal then please mention the reason for rejection which will be used in communication to the concerned business person or organization:
        ```
    - Text Area: 
        ```
        Message to the request creator
        ```

5. Save the form

The form should look like:


![](vx_images/2651595155596.png )
## Design the process

Now that we have the forms ready, we can design the process end to end:

1. Go to the main process: `${number} BP approval process`. Right now, it only has the trigger form:

    
    ![](vx_images/414432007888582.png )

2. Click in the ➕ button > _Approval_ > Select the `Business partner approval` approval form you just created

    
    ![](vx_images/550372836062569.gif )

    As a result, a new step with the approval is included. Note how this approval has two outputs.

 
    ![](vx_images/85792167016494.png )

3. Following the _Approve_ branch, click in the ➕ button > _Action_ > _Browse Library_

   
    
![](vx_images/219903093735858.gif )


4. Filter by your action project: `BP-API-${number}`, find _Creates a new Business Partner_ and click _Add_:

   
    
![](vx_images/365572532304845.png )
    As a result, a new step is added to the process.

5. To finish with this branch of the process, let's add the creation confirmation form:

    ![](vx_images/134663894909366.png )

    > [!NOTE]
    > Ignore the red mark 🔺 on each of the steps, we will take care of that later
    > 
    > 
 
![](vx_images/194955912921156.png )
    
6. Coming back to the approval, add a new mail step after _Reject_. This will trigger a mail notification:

   
    ![](vx_images/358445819668532.png )

    As a result, a new step is added:


![](vx_images/123046066569072.png )

> [!TIP|icon:fa-solid fa-check|label:Congratulations]
> You have successfully design the process. Save your progress.

## Bind data to forms, actions and mail

Now that the steps of the process are clear, let's complete the settings of each of them. What we will do is to tell SAP Build Process Automation how the data is going to move around the steps:

1. Click on the _Business partner approval_ step. You will see the missing information in red:

  
    ![](vx_images/163252665885371.png )

2. We can use the context data from the process to fill the fields:

    - For _Subject_:
        
        When pasting, right-click and choose _paste without formatting_ or _paste and match style_
        ```
        New business partner request for <Organization>
        ```

    ![](vx_images/315853198156979.gif )

    - For _Users_: Use your participant username to receive the tasks:

    ```
    user0${number}@domain.com
    ```

  
    
![](vx_images/489811839110392.png )
    > [!INFO]
    > For productive projects, we recommend assigning tasks to groups using _role collections_ of the subaccount, or groups from your Cloud Identity Service (IAS), read more in the documentation: [Guidelines for Specifying Recipient Users - SAP Build Process Automation](https://help.sap.com/docs/build-process-automation/sap-build-process-automation/guidelines-for-specifying-recipient-users?locale=en-US)


3. Still on _Business partner approval_, click on the tab _Inputs_ and map the inputs with the information coming from _Creation form (Trigger)_:

    
    ![](vx_images/27652879241518.png )

4. Moving to the next step, click in the **Action Creates a new business partner record**. Create a new destination variable:


![](vx_images/75016854771474.png )


This variable is a placeholder. When we deploy the project, you will assign an existing destination to this variable. Give it a meaningful name and click _Create_:
    
```
    s4hDestination
```

 
![](vx_images/39383980827016.png )

5. As before, go to the tab _Inputs_ and map the data to the API fields:

    
    ![](vx_images/461023581885702.png )

6. Continue with the _Creation confirmation_ form:

    - _Subject_:
        
        When pasting, right-click and choose _paste without formatting_ or _paste and match style_
        ```
        Congratulations! You have been successfully added as a business partner in our company
        ```
    - _Users_: Use your participant user email to receive the tasks:

    ```
    user0${number}@domain.com
    ```

    ![02-04-project-008](vx_images/4693405081406.png )

7. In the_Inputs_ tab, map the fields to the data. This time, we will include the business partner number coming from the S/4 system:

   
    
![](vx_images/161433428160824.png )

8. Finally, click on the _Send Mail_ step and fill the following:

    - To: Type a real email where you want to get the norification, or use your participant user email: `user0${number}@domain.com`
    - Subject: 
        ```
        [ATTENTION] Your business partner request has been rejected
        ```

    ![](vx_images/308592950734309.png )

9. To work on the mail body, click _Open Mail Body Editor_

 
    ![](vx_images/505201742444701.png )
    

    The editor will open.

10. Paste the following text and replace the placeholders with the actual variables:

    ```
    Dear <FirstName> <LastName>,
    
    Thank you for showing interest in working with us.
    
    Regrettably, your request for being a business partner with us has been rejected by the business partner manager, citing the following reason:
    
    <MessageToBusinessPartner>
    
    We'll be sure to contact you if any opportunity presents itself. Thank you again for your interest in working with us. We wish you success in your future endeavours.
    
    Best Regards,
    SAP Build Process Automation
    ```

   
    
![](vx_images/283742150629453.png )
11. Now all red marks are gone! Save the process.

  
![](vx_images/457542917570476.png )
> [!TIP|icon:fa-solid fa-check|label:Congratulations]
> The process is ready to be released and deployed. 

## Release and deploy the project

1. Click on the _Release_ button that is above the _Save_ button.

  
    
![](vx_images/22993557101076.png )
2. Because this is the first release, there is no need to change the version number. You can click _Release_:

 
    
![](vx_images/364923213842884.png )
    After the release, you can notice how the version number and the _Released_ tag appeared.

   
![](vx_images/532433124657080.png )
    This version of the project is now read only.

3. To deploy, click on the _Deploy_ button:

    ![](vx_images/92023841424431.png )

4. Select the _Public_ environment:
![](vx_images/233923104942544.png ))

5. Assign values to variables. Here is where you will assign the actual destination (the destination name might be different in your case):

![](vx_images/27784079551252.png )

6. The project will be deployed. When it finishes, you will see the tag _Deployed_:

 
    ![](vx_images/181852787995100.png )

> [!TIP|icon:fa-solid fa-check|label:Congratulations]
> You have successfully deployed the project.

## Test the process

1. Go to the main process: `${number} BP approval process`, and click once on the _Creation Form_. Copy the _Form link_:

 
    ![](vx_images/174353926221612.png )

2. Open the link in a new tab, the request form will show:

    ![](vx_images/316654332312325.png )

    Fill out the form and click _Submit_, at the bottom.


![](vx_images/471882358906085.png )
3. Go to SAP [SAP Build Lobby](https://build02-worksop.eu10.build.cloud.sap/) and access _My Inbox_:

    
![](vx_images/598594293392318.png )
4. You should have a new task awaiting approval. Verify that the information is OK, and click _Approve_ or _Reject_:

  
   ![](vx_images/501782799439313.png )

    If you approve, you will get a new task confirming the new business partner, including the business partner number:

    
   ![](vx_images/81923385523321.png )

    > [!NOTE|icon:fa-solid fa-camera|label:Screenshot]
    > Take a screenshot of the inbox showing the business partner creation confirmation. Click <a href="mailto:sap_btp_adoption_workshop@sap.com?subject=BUILD02_WORKSHOP_DAY_2_COMPLETION_USER0${number}&body=Please make sure the subject looks ok, and attach the screenshot before sending.">here</a> to create a new email. Send the screenshot to `sap_btp_adoption_workshop@sap.com`, including `BUILD02_WORKSHOP_DAY_2_COMPLETION_USER0${number}` as the subject.

    If you reject, you will get an email with the comment:

![](vx_images/373003740346367.png )
> [!TIP|icon:fa-solid fa-check|label:Congratulations]
> You have successfully built and tested a business process that interacts with an S/4 system with SAP Build Process Automation.