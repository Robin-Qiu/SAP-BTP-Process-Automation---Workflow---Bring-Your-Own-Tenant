<div class="draftWatermark"></div>


# 配置 API 触发器

---

在上一练习中，我们已构建并部署了业务流程。为了触发此流程，我们使用了表单。对于用户需要提供信息的简单场景，这是可行的。在许多其他情况下，您可能希望从另一个应用（如 Build Apps、Fiori 或其他应用）触发流程。要实现这一点，您可以使用 [API 触发器](https://help.sap.com/docs/build-process-automation/80e3d1a6e74844548a7d168fd1f95a98/configure-and-test-api-call-to-trigger-process)。

## 返回到 _可编辑_ 版本

1. 打开您的业务流程项目 `${number} BTP 创建流程`

![](vx_images/367103906151070.png)

2. 打开 _可编辑_ 版本：

   
    ![](vx_images/504764641953227.png )

## 创建数据类型

[数据类型](https://help.sap.com/docs/build-process-automation/80e3d1a6e74844548a7d168fd1f95a98/create-data-type-process-automation) 可以轻松管理一组字段。在本例中，我们可以将商业伙伴字段（firstName、lastName、email...）分组为一个 _商业伙伴_ 数据类型。

您将配置流程在通过 API 触发时期望包含这些字段。

1. 从项目概览中创建一个新的 _数据类型_：

  
    ![](vx_images/78535415836041.png )

2. 给出以下名称并点击 _创建_：

    ```
    商业伙伴
    ```

    ![](vx_images/221014330865879.png )

3. 下载数据类型 Excel 模板：[BPDataType.xlsx](https://robin-qiu.github.io/SAP-BTP-Process-Automation---Workflow---Bring-Your-Own-Tenant/vx_attachments/154271525142569/BPDataType.xlsx ':include')  :truck::truck::truck:. 
点击 _导入 Excel 文件_：

 
    
![](vx_images/420594567359013.png )
    > [!INFO]
    > 您也可以手动添加字段，但导入 Excel 会更快

4. 选择您刚刚下载的文件并点击 _导入 Excel 文件_：

    
![](vx_images/534144304362875.png )
5. 字段将被填充。它应该看起来像这样：

  
    
![](vx_images/77975241106541.png )
    > [!INFO]
    > 要定义一个数据类型，您必须添加它将包含的字段，并定义其类型（字符串、数字...）以及一些属性（如果它是值列表，是否为必填）。

6. 保存进度

> [!TIP|icon:fa-solid fa-check|label:恭喜]
> 您已成功创建数据类型。

## 更改触发器

1. 打开主流程项目 `${number} BTP 审批流程`

2. 点击触发表单上的三个点，然后点击 _移除_：

 
    ![](vx_images/350795979376239.png )

3. 现在添加一个新的 API 触发器：

    ![](vx_images/105066707134665.png )

4. 给它一个名称并点击 _创建_：

    ```
    API 触发器
    ```

    ![](vx_images/46335400826622.png )

5. 新的 API 触发器将如下所示：

 
![](vx_images/114567590797295.png )
> [!TIP|icon:fa-solid fa-check|label:恭喜]
> 您已成功配置了项目的 API 触发器。

## 配置流程的输入字段

当使用表单作为触发器时，用户会被要求填写相关字段。为了实现同样的效果，我们需要定义流程的输入。

1. 点击灰色区域的任意位置以查看右侧的 _流程详情_。点击 _变量_。在 _流程输入_ 旁边，点击 _配置_：

  
    ![](vx_images/527623646168120.png )

2. 点击 _添加输入_，给出以下名称。在 _类型_ 中选择 _商业伙伴_（列表底部）。将其标记为必填。点击 _应用_。

    ```
    商业伙伴输入
    ```

    ![](vx_images/504703895692319.png )

3. 保存进度

> [!TIP|icon:fa-solid fa-check|label:恭喜]
> 您已成功配置了流程的输入参数。

## 在流程的其余部分映射新字段

当您删除了 _创建表单_ 触发器后，所有在审批、操作和邮件步骤中对字段的映射都消失了。使用流程输入中可用的新字段重新配置这些映射。

1. 映射审批表单中的字段

    - 在 _通用_ 选项卡中：在 _主题_ 字段末尾添加组织名称：

 
    ![](vx_images/111764028472472.png )

    - 在 _输入_ 选项卡中：映射所有字段

    ![](vx_images/226805811273743.png )


2. 映射操作中的字段

    - 在 _输入_ 选项卡中：映射所有字段

    ![](vx_images/357745151756306.png )

3. 映射邮件中的字段

    - 点击 _打开邮件编辑器_：在称呼中添加姓名和姓氏：

   
    ![](vx_images/483496030621654.png )

4. 保存项目。

## 发布并部署项目

1. 点击位于 _保存_ 按钮上方的 _发布_ 按钮。

   
    ![](vx_images/118494152904830.png )

2. 由于这是首次发布，无需更改版本号。您可以点击 _发布_：

   
    ![](vx_images/232434169620911.png )

    发布后，您会注意到版本号和 _已发布_ 标签的出现。

  
![](vx_images/464185765199237.png )
    该项目的此版本现在只读。

3. 要部署，请点击 _部署_ 按钮：

    ![](vx_images/591944278090281.png )
    ![](vx_images/284644668768149.png )
    ![](vx_images/524355285022421.png )

    这是一个三步过程：

    1. 审查将被部署的组件，点击 _下一步_：

    ![](vx_images/105976225027121.png )

    2. 为变量分配值。在这里，您将分配实际的目标（目标名称可能因情况而异）：

  
![](vx_images/105694047262698.png )

    3. 审查触发器。现在您可以看到您创建的 API 触发器。点击 _部署_：

  ![](vx_images/221235940896906.png )

    项目将被部署。部署完成后，您将看到 _已部署_ 标签：

  
![](vx_images/527325875755688.png )
> [!TIP|icon:fa-solid fa-check|label:恭喜]
> 您已成功部署项目。

## 配置 SAP 商业加速器中心以进行 API 测试

现在项目已准备就绪并等待 API 请求。让我们利用 SAP 商业加速器中心来触发 API 请求。

1. 打开 [SAP 商业加速器中心](https://api.sap.com/) 并使用您的 BTP 账户登录。然后点击 **SAP 商业技术平台** 标签页以浏览 BTP API：

    ![](vx_images/234916419544413.png )
2. 打开 **APIs** 标签页，搜索 ***"workflow"***，然后点击 **SAP Build Process Automation** 标签页以找到工作流 API：

![](vx_images/407057753270463.png )

3. 在 **REST API** 标签页中，点击 **Workflow** 标签页并打开 API 规格。
![](vx_images/38297283116954.png )

4. 在 **API 参考** 标签页中，打开 **Workflow Instances** 菜单以检查 API。
![](vx_images/448946071958656.png )



## 配置 API 测试环境

您可以使用 Postman 或 Insomnia 等免费桌面工具发送 API 请求。  
在本练习中，您将利用 SAP 商业加速器中心来测试 API。

首先，您需要为您的许可产品设置环境，以便使用您的数据测试 API。

1. 点击 **尝试** 标签页，然后选择 **选择环境** 以 **添加新环境**。
![](vx_images/220361793846198.png )

2. 输入 **显示名称**，并选择指向您子账号 API 端点的 **起始 URL**。

![](vx_images/142942203635290.png )

![](vx_images/438463326961041.png )

3. 在 **认证** 部分下输入 OAuth2.0 配置，您可以在 SAP Build Process Automation 实例的密钥中找到 *客户端 ID*、*客户端密钥* 和 *令牌 URL*。在 **消费者子域名** 字段中，您可以参考实例密钥中的 **身份域**。
> [!INFO]
> 更多关于如何获取 OAuth2.0 客户端凭据详情，请参阅文档：[确定服务配置参数 - SAP Build Process Automation](https://help.sap.com/docs/build-process-automation/80e3d1a6e74844548a7d168fd1f95a98/determine-service-configuration-parameters)

![](vx_images/228634528596087.png)
![](vx_images/78445827142565.png)
![](vx_images/152405386827095.png)

## 测试 API 触发器

1. 返回 **尝试** 标签页，选择您的测试环境，并在 **工作流实例** 菜单下选择 API */v1/workflow-instances*。

粘贴请求体如下：
```
{
    "definitionId": "<<从监控页面获取>>",
    "context": {
        "businessPartnerInput": {
            "firstName": "John",
            "lastName": "Doe",
            "email": "johndoe@example.com",
            "category": "1",
            "organization": "Acme Inc.",
            "initials": "JD",
            "searchTerm": "johndoe",
            "additionalComment": "thanks in advance"
        }
    }
}
```

![](vx_images/348607218921235.png )

打开监控菜单，点击 **流程和工作流** 标签页以检查已部署的工作流。
![](vx_images/195061815542775.png )

**ID** 将在请求有效载荷中作为 **definitioId** 使用
![](vx_images/421753026668611.png )

2. 成功响应应如下所示：
![](vx_images/31623673569151.png )

3. 从 SAP [SAP Build 大厅](https://build02-worksop.eu10.build.cloud.sap/) 进入 _我的收件箱_。

![](vx_images/278974725654399.png )
5. 您将看到新任务：

![](vx_images/415086289310000.png )

> [!TIP|icon:fa-solid fa-check|label:恭喜]
> 您已成功配置、部署并测试了 SAP Build Process Automation 中的 API 触发器。