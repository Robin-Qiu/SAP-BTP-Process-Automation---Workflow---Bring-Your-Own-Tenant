# Add app and trigger form into SAP Build Work Zone, Standard Edition


### Create an instance for SAP Build Process Automation

Once you have successfully subscribed to **SAP Build Process Automation** in **SAP BTP Cockpit**, you can find the subscription in your sub account view, under **Instances and Subscriptions**.
![](vx_images/172181640510670.png )

1. Let’s create an Instance for SAP Build Process Automation. Choose **Create**.

2. Select the Service as **SAP Build Process Automation** and Plan as `standard` instance.
![](vx_images/299192199762755.png )
3. Enter the values for other fields as shown below and give an instance name as spa-instance. Choose **Create**.

|  Field	   |  Value   |
| --- | --- |
|  Service   |   SAP Build Process Automation  |
|   Plan  |   standard - Instance  |
|  Runtime Environment   |   Cloud Foundry  |
|   Space  |  dev   |
|  Instance Name   |  any name (spa-instance)   |

 
![](vx_images/102462926708265.png )
	
	
	
	
4. Once the instance is created successfully, you can find it in **Instances** section.
![](vx_images/599824477768230.png )


---
### Create a service key for the instance of SAP Build Process Automation

1. Once you have successfully created the instance, select **… > Create Service Key**.
![](vx_images/529785394022502.png )

2. Enter the name for Service Key as **spa-key **and choose **Create**.
![](vx_images/469664056262779.png )


3. The service key is created and you can view the credentials.
![](vx_images/267924433177592.png )

4. After the key is provisioned, open it and take note of the following fields:

* **api**
* **clientid**
* **clientsecret**
* **url**

These values are needed later in the Destination Configuration section.
![](vx_images/67196049896987.png )

---
### Create a destination to trigger process

1. Navigate to **Destinations > Create Destination**. Enter the destination name as `sap_process_automation_service`.

> [!NOTE]
>  **During the workshop, the trainer will supply the destination template to you. You can import it and modify the parameters accordingly.**
> 

![](vx_images/546523271915551.png )

2. Enter the details as below.

|             Field              |                                                                                                           Value                                                                                                           |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Name                           | any name (`sap_process_automation_service`)                                                                                                                                                                               |
| Type                           | HTTP                                                                                                                                                                                                                      |
| Description                    | any description                                                                                                                                                                                                           |
| URL                            | 	`api/public/workflow/rest/v1/workflow-instances`, where `api` is noted previously in step 2,     such as: `https://spa-api-gateway-bpi-us-prod.cfapps.us10.hana.ondemand.com/public/workflow/rest/v1/workflow-instances` |
| Proxy Type                     | Internet                                                                                                                                                                                                                  |
| Authentication                 | OAuth2ClientCredentials                                                                                                                                                                                                   |
| Use `mTLS` for token retrieval | Off                                                                                                                                                                                                                       |
| Client ID                      | Paste the client id noted previously in step 2                                                                                                                                                                            |
| Client Secret                  | Paste the client secret noted previously in step 2                                                                                                                                                                        |
| Token Service URL Type         | Dedicated                                                                                                                                                                                                                 |
| Token Service URL              | `url/oauth/token`, where `url` is noted previously in step 2,          The final URL should be something like this:  `https://<your tenant>.authentication.<domain>.hana.ondemand.com/oauth/token`                        |
| Token Service User             | Blank                                                                                                                                                                                                                     |
| Token Service Password         | Blank                                                                                                                                                                                                                     |

> [!TIP] 
> Additionally, enable the following properties when you would like to integrate with SAP Build Apps.

Then, copy over and add the following additional properties from the service key:

|          Field          |                                 Value                                 |
| ----------------------- | --------------------------------------------------------------------- |
| endpoints               | endpoints (copy the whole JSON structure including ‘{‘ and ‘}’)       |
| html5-apps-repo         | html5-apps-repo (copy the whole JSON structure including ‘{‘ and ‘}’) |
| saasregistryenabled     | saasregistryenabled copied from the service key                       |
| sap.cloud.service       | sap.cloud.service copied from the service key                         |
| sap.cloud.service.alias | sap.cloud.service.alias copied from the service key                   |

![](vx_images/23452466133179.png )

You have successfully created a destination and you can trigger your business process from any service like SAP Build Work Zone, Standard Edition.

3. Test the destination

When you will check the connection to the destination, the status will show **401: Unauthorized**.

>  
> Even though the connection returns unauthorized, the status is successful.
>  

![](vx_images/358227099635294.png )


---
### Create a Site Using SAP Build Work Zone, standard edition
> 
> **Prerequisites**
> You have subscribed to SAP Build Work Zone, standard edition and assigned yourself to the `Launchpad_Admin` role
> 

When you access the SAP Build Work Zone, standard edition, the Site Directory is in focus. From here you’ll create your new site.

> In the side panel, you’ll see four tools. The **Site Directory** where you’re going to create a new site. All sites that you create will be displayed here. The **Content Manager** where you’ll manage cross-site content such as business apps. The **Channel Manager** where you manage different channels that expose business content that you can integrate into your sites. The fourth icon opens **Settings** where you can configure various settings related to your subaccount.




1. In the side navigation panel of your subaccount, click **Instances and Subscriptions** and then next to **SAP Build Work Zone, standard edition**, click the **Go to Application** icon.
![](vx_images/172354325254376.png )


2. Click **Create Site**.

![](vx_images/337075593434869.png )

3. Enter `Demo` as the site name and click **Create**.
![](vx_images/234786889065268.png )


You’ve just created a site called `Demo`.

4. lick the Channel Manager icon to view any available content providers.

![](vx_images/238725493558625.png )

5. Select the HTML5 Apps content provider.

> The **HTML5 Apps** content provider is created automatically. Any app that you deploy to SAP BTP is automatically added as content to this provider.

![](vx_images/508215802671924.png )


6. Click the **Fetch updated content** icon.
![](vx_images/261366837587053.png )

The **HTML5 Apps** content provider should now expose any newly deployed app for integration.

        
            

---
### Add your deployed SAP Build Process Automation Form to your content

1. Click the icon in the side panel to open the **Content Manager**.
![](vx_images/74866856937307.png )


> The **Content Manager** has two tabs: **My Content** where you can manually configure content items and view any other available content items, and the **Content Explorer** where you can explore exposed content from available content providers, select the content, and add it to your own content.


2. Click the **Content Explorer** tab to explore content from the available content providers.
![](vx_images/105542801900152.png )


3. Select the **HTML5 Apps** provider.
![](vx_images/47631988832543.png )

4. You’ll see that  **My Inbox**, **Process Trigger** created by SAP Build Process Automation, already exist in this provider. Select them and click **Add**.
![](vx_images/519182256649532.png )



5. Click the **Content Manager** tab.
![](vx_images/7584048771557.png )

> [!NOTE]
> Note that `My Inbox, Process Triggers` are in the list of content items.

---  
  
### Create group and assign app to it

In this step, you’ll create a new group and assign the `My Inbox, Process Triggers` apps to it.

> A group is a set of one or more apps displayed together in a site. Assigning apps to groups, makes them visible to the user.

1. Click **+ New** in the **Content Manager** and select **Group** to create a new group.
![](vx_images/38892398970611.png )

2. Enter Our `Demo` as the **Title**.


3. In the **Assignments** panel on the right, click in the search box to see a list of apps.

> If you have many apps, you can type some letters of your app name in the search bar, (for example, `My`) to search for the app.

4. Next to the `My Inbox` app, click the + icon to assign your app to this group.
![](vx_images/187773566065179.png )


You’ll see that the icon changes.

5. Click **Save**.
![](vx_images/434683745200165.png )

---
### Assign app to Everyone role
In this step, you’ll assign the `My Inbox` app to the `Everyone` role. This is a default role - content assigned to the `Everyone` role is visible to all users.

1. Open the **Content Manager** from the side panel.
![](vx_images/460582833321367.png )

2. Click the `Everyone` role to open the role editor.
![](vx_images/253792953462902.png )


3. Click **Edit**.
![](vx_images/43232166261097.png )


4. Click the search box in the **Apps** panel. Any available apps are shown in the list below.
5. Next to the `My Inbox` app, click the **Switch** icon. You’ll see that the icon changes.
6. Click **Save**.
![](vx_images/95953614304063.png )

---

### Review your site

1. Click the **Site Directory** icon to open the Site Directory.
![](vx_images/18743293025836.png )


2. Click **Go to site** on the site tile.
![](vx_images/254672477917749.png )

You’ll see all the apps that you have created in your site. In the `Demo` group, you’ll see the `My Inbox` app that we’ve just created.
![](vx_images/145051513544495.png )

3. Click the app to launch it.
![](vx_images/435082047270545.png )

---

### Create reques form basing on Process Trigger template

1. Click **Content Manager** menu and choose **Process Trigger**
![](vx_images/40482776117036.png )

2. Click **Create a Local Copy**
![](vx_images/281071264958738.png )

3. Click Edit to modify the app tile
![](vx_images/577682853754188.png )

* Enter `Request Form` as the new title
![](vx_images/458743258674283.png )


* Choose the **Navigation** tab and copy the `Launchpad Configuration Parameter` from deployed process and paste it to `uri` parameter.
![](vx_images/119922642656755.png )



* Choose **Visualization** tab. Enter `Business Partner` as **Subtitle**, and enter `SPA Exercise` as **Information**.
![](vx_images/340153601682860.png )

* Choose **Translation** tab and change the **Translated Text** accordingly.
Click **Save** button
![](vx_images/359683573646195.png )


4. Repeat above group and role assignment steps and the `Request Form` will be under `Demo` group and `Everyone` role.

![](vx_images/391255307289775.png )

![](vx_images/192434460419344.png )


5. Open the `Demo` site to check the result.
![](vx_images/556795291160284.png )

---
### Test to submit one request form
1. Open the Request Form app
![](vx_images/111925380057349.png )

2. Fill in the required fields and submit the form
![](vx_images/356075583425435.png )

3. Check the new task in the **My Inbox**
![](vx_images/63984812309113.png )


> ###### Congratulations to you! :tada: :tada: :tada: 
> You've finished the integration exercise and you can leverage SAP Build Work Zone, Standard Edition as app portal to integrate other BTP services.