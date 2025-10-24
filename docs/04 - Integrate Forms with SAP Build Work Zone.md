<div class="draftWatermark"></div>


# 在 SAP Build Work Zone 标准版中添加应用和触发表单

---

### 为 SAP Build Process Automation 创建实例

一旦您在 **SAP BTP 控制台** 中成功订阅了 **SAP Build Process Automation**，您可以在您的子账号视图中，于 **实例和订阅** 下找到该订阅。

![](vx_images/172181640510670_1.png )

1. 让我们为 SAP Build Process Automation 创建一个实例。选择 **创建**。

2. 选择服务为 **SAP Build Process Automation**，计划为 `standard` 实例。
![](vx_images/299192199762755_1.png )
3. 填写其他字段的值，如下所示，并将实例名称设为 spa-instance。选择 **创建**。

|  字段	   |  值   |
| --- | --- |
|  服务   |   SAP Build Process Automation  |
|   计划  |   standard - Instance  |
|  运行时环境   |   Cloud Foundry  |
|   空间  |  dev   |
|  实例名称   |  任意名称 (spa-instance)   |

 
![](vx_images/102462926708265_1.png )
	
	
	
	
4. 一旦实例成功创建，您可以在 **实例** 部分找到它。
![](vx_images/599824477768230_1.png )


---
### 为 SAP Build Process Automation 的实例创建服务密钥

1. 一旦成功创建实例，选择 **… > 创建服务密钥**。

![](vx_images/529785394022502_1.png )

2. 为服务密钥输入名称 `spa-key`，然后选择 **创建**。

![](vx_images/469664056262779_1.png )


3. 服务密钥已创建，您可以查看凭据。
![](vx_images/267924433177592_1.png )

4. 密钥生成后，打开它并注意以下字段：

* **api**
* **clientid**
* **clientsecret**
* **url**

这些值将在后续的 Destination 配置部分使用。 

![](vx_images/67196049896987_1.png )

---
### 创建目的地以触发流程

1. 导航到 **目的地 > 创建目的地**。将目的地名称设为 `sap_process_automation_service`。

> [!NOTE]
>  在工作坊期间，培训师将为您提供目的地模板。您可以导入它并相应地修改参数。[sap_process_automation_service](https://robin-qiu.github.io/SAP-BTP-Process-Automation---Workflow---Bring-Your-Own-Tenant/vx_attachments/154271525142569/sap_process_automation_service ':include')  :truck::truck::truck:. 
> 

![](vx_images/546523271915551_1.png )

2. 填写以下详细信息。

|             字段              |                                                                                                           值                                                                                                           |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 名称                           | 任意名称 (`sap_process_automation_service`)                                                                                                                                                                               |
| 类型                           | HTTP                                                                                                                                                                                                                      |
| 描述                          | 任意描述                                                                                                                                                                                                               |
| URL                           |  `api/public/workflow/rest/v1/workflow-instances`，其中 `api` 是之前第 2 步中提到的，例如：`https://spa-api-gateway-bpi-us-prod.cfapps.us10.hana.ondemand.com/public/workflow/rest/v1/workflow-instances` |
| 代理类型                     | Internet                                                                                                                                                                                                                  |
| 认证                         | OAuth2ClientCredentials                                                                                                                                                                                                   |
| 使用 mTLS 进行令牌获取       | 关闭                                                                                                                                                                                                                     |
| 客户端 ID                      | 粘贴之前第 2 步中提到的客户端 ID                                                                                                                                                                                         |
| 客户端密钥                  | 粘贴之前第 2 步中提到的客户端密钥                                                                                                                                                                                         |
| 令牌服务 URL 类型           | 专用                                                                                                                                                                                                                 |
| 令牌服务 URL                | `url/oauth/token`，其中 `url` 是之前第 2 步中提到的，最终 URL 应类似于：`https://<your tenant>.authentication.<domain>.hana.ondemand.com/oauth/token`                        |
| 令牌服务用户               | 留空                                                                                                                                                                                                                     |
| 令牌服务密码               | 留空                                                                                                                                                                                                                     |

> [!TIP] 
> 此外，当您希望与 SAP Build Apps 集成时，请启用以下属性。

然后，复制并添加以下额外属性来自服务密钥：

|          字段          |                                 值                                 |
| ----------------------- | --------------------------------------------------------------------- |
| endpoints               | endpoints（复制整个 JSON 结构，包括‘{’和‘}’）                       |
| html5-apps-repo         | html5-apps-repo（复制整个 JSON 结构，包括‘{’和‘}’）                   |
| saasregistryenabled     | saasregistryenabled 复制自服务密钥                                  |
| sap.cloud.service       | sap.cloud.service 复制自服务密钥                                   |
| sap.cloud.service.alias | sap.cloud.service.alias 复制自服务密钥                              |

![](vx_images/23452466133179_1.png )

您已成功创建了一个目的地，可以从任何服务（如 SAP Build Work Zone 标准版）触发您的业务流程。

3. 测试目的地

当您检查与目的地的连接时，状态将显示为 **401: 未授权**。

>  
> 尽管连接返回未授权，但状态是成功的。
>  

![](vx_images/358227099635294_1.png )


---
### 使用 SAP Build Work Zone 标准版创建站点
> 
> **前提条件**
> 您已订阅 SAP Build Work Zone 标准版，并已将自己分配到 `Launchpad_Admin` 角色
> 

当您访问 SAP Build Work Zone 标准版时，站点目录将处于焦点。从这里，您将创建新的站点。

> 在侧面面板中，您将看到四个工具。**站点目录**，您将在此创建新站点。您创建的所有站点都将在此显示。**内容管理器**，您将在此管理跨站点内容，例如业务应用。**渠道管理器**，您将在此管理不同渠道，这些渠道暴露业务内容，可用于集成到您的站点中。第四个图标打开**设置**，您可以在其中配置与子账号相关的各种设置。

1. 在子账号的侧面导航面板中，点击 **实例和订阅**，然后在 **SAP Build Work Zone，标准版** 旁边点击 **进入应用** 图标。

![](vx_images/172354325254376_1.png )


2. 点击 **创建站点**。

![](vx_images/337075593434869_1.png )

3. 将 `Demo` 作为站点名称，然后点击 **创建**。

![](vx_images/234786889065268_1.png )


您刚刚创建了一个名为 `Demo` 的站点。

4. 点击渠道管理器图标以查看任何可用的内容提供商。

![](vx_images/238725493558625_1.png )

5. 选择 HTML5 Apps 内容提供商。

> **HTML5 Apps** 内容提供商将自动创建。您部署到 SAP BTP 的任何应用将自动添加到此提供商中作为内容。

![](vx_images/508215802671924_1.png )


6. 点击 **获取最新内容** 图标。

![](vx_images/261366837587053_1.png )

**HTML5 Apps** 内容提供商现在应暴露任何新部署的应用，以便集成。

        
            

---
### 将已部署的 SAP Build Process Automation 表单添加到您的内容中

1. 点击侧面面板中的图标以打开 **内容管理器**。
![](vx_images/74866856937307_1.png )


> **内容管理器** 有两个标签页：**我的内容**，您可以手动配置内容项并查看其他可用内容项；以及**内容探测器**，您可以探索来自可用内容提供商的暴露内容，选择内容并将其添加到自己的内容中。

2. 点击 **内容探测器** 标签页以探索来自可用内容提供商的内容。
![](vx_images/105542801900152_1.png )


3. 选择 **HTML5 Apps** 提供商。
![](vx_images/47631988832543_1.png )

4. 您将看到 **My Inbox** 和 **Process Trigger**（由 SAP Build Process Automation 创建）已经存在于此提供商中。选择它们并点击 **添加**。

![](vx_images/519182256649532_1.png )



5. 点击 **内容管理器** 标签页。
![](vx_images/7584048771557_1.png )

> [!NOTE]
> 请注意，`My Inbox, Process Triggers` 已出现在内容项列表中。

---  
  
### 创建组并将其分配给应用

在本步骤中，您将创建一个新组并将 `My Inbox, Process Triggers` 应用分配给该组。

> 组是一组一个或多个应用，它们在站点中一起显示。将应用分配给组，会使它们对用户可见。

1. 在 **内容管理器** 中点击 **+ 新建**，然后选择 **组** 以创建新组。
![](vx_images/38892398970611_1.png )

2. 输入 `Our Demo` 作为 **标题**。

3. 在右侧的 **分配** 面板中，点击搜索框以查看应用列表。

> 如果您有多个应用，可以在搜索栏中输入应用名称的一部分（例如，`My`）来搜索应用。

4. 在 `My Inbox` 应用旁边，点击加号图标以将您的应用分配给此组。
![](vx_images/187773566065179_1.png )


您会看到图标发生了变化。

5. 点击 **保存**。

![](vx_images/434683745200165_1.png )

---
### 将应用分配给 Everyone 角色
在本步骤中，您将把 `My Inbox` 应用分配给 `Everyone` 角色。这是一个默认角色 - 分配给 `Everyone` 角色的内容对所有用户可见。

1. 从侧面面板打开 **内容管理器**。

![](vx_images/460582833321367_1.png )

2. 点击 `Everyone` 角色以打开角色编辑器。

![](vx_images/253792953462902_1.png )


3. 点击 **编辑**。

![](vx_images/43232166261097_1.png )


4. 点击 **Apps** 面板中的搜索框。下面的列表中将显示所有可用应用。
5. 在 `My Inbox` 应用旁边，点击 **切换** 图标。您将看到图标发生变化。
6. 点击 **保存**。
![](vx_images/95953614304063_1.png )

---

### 查看您的站点

1. 点击 **站点目录** 图标以打开站点目录。
![](vx_images/18743293025836_1.png )


2. 点击站点标签上的 **进入站点**。
![](vx_images/254672477917749_1.png )

您将看到您在站点中创建的所有应用。在 `Demo` 组中，您将看到我们刚刚创建的 `My Inbox` 应用。
![](vx_images/145051513544495_1.png )

3. 点击该应用以启动它。

![](vx_images/435082047270545_1.png )

---

### 基于流程触发模板创建请求表单

1. 点击 **内容管理器** 菜单，选择 **流程触发**。
![](vx_images/40482776117036_1.png )

2. 点击 **创建本地副本**。

![](vx_images/281071264958738_1.png )

3. 点击 **编辑** 以修改应用标签。

![](vx_images/577682853754188_1.png )

* 将新标题设为 `Request Form`

![](vx_images/458743258674283_1.png )


* 选择 **导航** 选项卡，并从已部署的流程中复制 **启动页配置参数**，然后粘贴到 `uri` 参数中。
![](vx_images/119922642656755_1.png )



* 选择 **可视化** 选项卡。将 `Business Partner` 设为 **副标题**，将 `SPA Exercise` 设为 **信息**。
![](vx_images/340153601682860_1.png )

* 选择 **翻译** 选项卡并相应更改 **翻译文本**。点击 **保存** 按钮
![](vx_images/359683573646195_1.png )


4. 重复上述组和角色分配步骤，请求表单将位于 `Demo` 组和 `Everyone` 角色下。

![](vx_images/391255307289775_1.png )

![](vx_images/192434460419344_1.png )


5. 打开 `Demo` 站点以检查结果。

![](vx_images/556795291160284_1.png )

---
### 测试提交一个请求表单
1. 打开请求表单应用

![](vx_images/111925380057349_1.png )

2. 填写所需字段并提交表单

![](vx_images/356075583425435_1.png )

3. 检查 **My Inbox** 中的新任务

![](vx_images/63984812309113_1.png )


> ###### 恭喜您！ :tada: :tada: :tada: 
> 您已完成集成练习，现在可以利用 SAP Build Work Zone 标准版作为应用门户，集成其他 BTP 服务。