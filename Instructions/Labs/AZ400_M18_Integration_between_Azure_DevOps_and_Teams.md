---
lab:
    title: '实验室 18： Azure DevOps 和 Teams 的集成'
    module: '模块 18：实现系统反馈机制'
---

# 实验室 18： Azure DevOps 和 Teams 的集成
# 学生实验室手册

## 实验室概述

**[Microsoft Teams](https://teams.microsoft.com/start)** 是 Office 365 中团队合作的中心。使用它，可以在一处管理和使用团队的所有聊天、会议、文件和应用。它为软件开发团队提供了一个协作中心，使其能够跨 Office 365 和 Azure DevOps 实现团队合作、沟通交流、共享内容和使用工具。

在本实验室中，你将实现 Azure DevOps 服务和 Microsoft Teams 之间的集成方案。

> **备注**：**Azure DevOps 服务**与 Microsoft Teams 集成，在整个开发周期中提供复合聊天和协作体验。通过工作项、拉取请求、代码提交以及生成和发布事件的通知和警报，可使团队随时了解 Azure DevOps 团队项目中的重要活动。

## 目标

完成本实验室后，你将能够：

- 集成 Microsoft Teams 与 Azure DevOps
- 集成 Azure DevOps 看板和 Teams 中的仪表板
- 集成 Azure Pipelines 与 Microsoft Teams
- 在 Microsoft Teams 中安装 Azure Pipelines 应用
- 订阅 Azure Pipelines 通知

## 实验室持续时间

-   预计用时：**60 分钟**

## 说明

### 准备工作

#### 登录到实验室虚拟机

确保已使用以下凭据登录到 Windows 10 计算机：
    
-   用户名：**Student**
-   密码：**Pa55w.rd**

#### 查看本实验室所需的应用程序

确定你将在本实验室中使用的应用程序：
    
-   Microsoft Edge
-   Microsoft Teams。此应用程序将作为本实验室先决条件安装。

#### 设置 Office 365 订阅 

从 [Microsoft Teams 注册页](https://teams.microsoft.com/start)创建免费试用版订阅。 

#### 设置 Azure DevOps 组织。 

遵循[创建组织或项目集合](https://docs.microsoft.com/zh-cn/azure/devops/organizations/accounts/create-organization?view=azure-devops)中的说明。创建 Azure DevOps 组织时，使用你用于设置 Office 365 订阅的用户帐户登录。

> **备注**：你的 Office 365 订阅和 Azure DevOps 组织必须共享相同的 Azure Active Directory (Azure AD) 租户。

### 练习 0：配置实验室先决条件

在本练习中，你将设置实验室先决条件，包括预先配置的 **Tailwind Traders** 团队项目，它基于 Azure DevOps 演示生成器模板和在 Microsoft Teams 中创建的团队。

#### 任务 1：配置团队项目

在此任务中，你将使用 Azure DevOps 演示生成器，基于 **Tailwind Traders** 模板生成新项目。

1.  在实验室计算机上，启动 Web 浏览器并导航到 [Azure DevOps 演示生成器](https://azuredevopsdemogenerator.azurewebsites.net)。此实用工具将对以下过程进行自动化：在你的帐户中创建预填充了实验室所需内容（工作项、存储库等）的 Azure DevOps 项目。 

    > **备注**：有关该站点的详细信息，请参阅 https://docs.microsoft.com/zh-cn/azure/devops/demo-gen。

1.  单击“**登录**”，并使用与你的 Azure DevOps 订阅相关联的 Microsoft 帐户登录。
1.  如果需要，在“**Azure DevOps 演示生成器**”页面上，单击“**接受**”以接受访问 Azure DevOps 订阅的权限请求。
1.  在“**创建新项目**”页面上，单击“**选择模板**”。
1.  在模板列表中，单击工具栏中的“**常规**”，选择“**Tailwind Traders**”，然后单击“**选择模板**”。
1.  返回“**创建新项目**”页面，在“**新建项目名称**”文本框中键入“**Tailwind Traders**”，然后在“**选择组织**”下拉列表中选择你的 Azure DevOps 组织。
1.  在“**创建新项目**”页面上，如果系统提示你安装缺少的扩展，请选中“**ARM 输出**”下方的复选框，然后单击“**创建项目**”（忽略 GitHub 分支）。

    > **备注**：等待此过程完成。该过程大约需要 2 分钟。如果该过程失败，请导航到你的 DevOps 组织，删除项目并重试。

1.  在 **“新建项目”** 页面上，单击 **“导航到项目”**。

#### 任务 2：在 Microsoft Teams 中创建团队。

在此任务中，你将在 Microsoft Teams 中创建团队。

1.  在实验室计算机上，启动 Web 浏览器，导航到 [Microsoft Teams 下载页](https://www.microsoft.com/zh-cn/microsoft-365/microsoft-teams/download-app)，然后从该页面下载 Microsoft Teams 并以默认设置安装它。 
1.  在实验室计算机上，使用桌面应用启动 **Microsoft Teams**。

    > **备注**：你还可以使用 Web 浏览器并导航到 [Microsoft Teams 登录页](https://teams.microsoft.com/dl/launcher/launcher.html?url=/_%23/l/home/0/0&type=home)

1.  提示登录时，使用属于 Office 365 订阅且有权访问你的 Azure DevOps 组织的用户帐户登录。
1.  在 Microsoft Teams 中，在页面左侧的工具栏中单击 **“Teams”**，然后在团队列表底部单击 **“加入或创建团队”**。

    >**备注**：团队即围绕共同目标进行协作的一群人。 

1.  在 **“加入或创建团队”** 窗格上，单击 **“创建团队”**。
1.  在 **“创建团队”** 窗格上单击 **“从头开始”**，在 **“这会是什么类型的团队？”** 窗格上单击 **“私密”**
1.  在 **“有关私密团队的简要信息”** 面板上，将 **“为你的团队命名”** 替换为 **“Tailwind Traders”** 并单击 **“创建”**。
1.  在 **“向 Tailwind Traders 添加成员”** 面板上，单击 **“跳过”**。

### 练习 1：集成 Azure Boards 与 Microsoft Teams

在此练习中，你将实现 Azure Boards和 Microsoft Teams 之间的集成。

#### 任务 1：在 Microsoft Teams 中安装并配置 Azure Boards 应用

在此任务中，你将在 Microsoft Teams 中新创建的团队中安装并配置 Azure Boards 应用。

1.  在 Microsoft Teams 窗口的左下角，单击 **“应用”** 图标。这将打开 **“应用”** 窗格。
1.  在 **“应用”** 窗格上的 **“搜索所有应用”** 文本框中键入 **“Azure Boards”**，然后在应用列表中单击 **“Azure Boards”**。
单击“**打开**”按钮右侧的向下箭头，然后在下拉列表中选择“**添加到团队**”条目。
1.  在“**为团队设置 Azure Boards**”面板的“**搜索**”文本框中，键入“**Tailwind Traders**”。从搜索结果中选择“**Tailwind Traders**”>“**常规**”条目，然后单击“**设置机器人**”。

1.  从“**Tailwind Traders**”团队的“**常规**”频道的帖子列表中，选择标题为“**Azure Boards**”的帖子，然后按 **Enter** 键查看机器人发布的其他消息，如下所示：

    ```
    Here are some of the things you can do:
    link [project url] - Link to a project to create work items and receive notifications
    subscriptions - Add or remove subscriptions for this channel
    addAreapath [area path] - Add an area path from your project to this channel
    signin - Sign in to your Azure Boards account
    signout - Sign out from your Azure Boards account
    unlink - Unlink a project from this channel
    feedback - Report a problem or suggest a feature
    To know more see documentation.
    ```
1.  打开“**新对话**”并键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Boards**”，然后在命令面板中选择“**登录**”。按照以下步骤，确保你有权访问 Azure DevOps 组织。
1.  复制 Azure DevOps“**Tailwind Traders**”项目的 url。例如：https://dev.azure.com/myorg/myproject。在 Teams 频道中打开“**新对话**”并键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Boards**”，然后在命令面板中选择“**链接**”。此时，粘贴已复制的项目 url。你的帖子应如下所示： 
´**Azure Boards** link https://dev.azure.com/myorg/myproject ´。按 **Enter**。

    查看收到的消息：

    ```
    NAME has linked this channel to project  Tailwind Traders. Create work items using @Azure         Boards create.
    To monitor work items, please add subscription
    Add subscription
    ```

1. 单击“**添加订阅**”。在下拉列表中，从事件列表中选择“**创建的工作项**”并单击“**下一步**”。保留默认值并单击“**提交**”。单击“**确定**”并关闭。频道中将发布一条消息，其中包含关于新添加的订阅的详细信息。
1.  切换到在 Azure DevOps 门户中显示“**Tailwind Traders**”项目的 Web 浏览器，单击“**Boards**”>“**工作项**”。单击“**新建工作项**”，然后从下拉列表中选择“**用户情景**”。为用户情景提供一个标题（例如“**测试 Azure Boards 与 Teams 的集成**”）并**保存**。我们最近设置的 Teams 频道会发布一个通知/卡片，其中包含关于创建的用户情景的信息。

#### 任务 2： 将 Azure Boards 看板添加到 Microsoft Teams

在此任务中，你要将 Azure Boards 看板添加到 Microsoft Teams 中的选项卡。

> **备注**：看板会将你的积压工作 (backlog) 变为交互式布告板，提供视觉工作流。随着工作从创意阶段进行到完成，你将更新面板上的项。每一列代表一个工作阶段，每张卡片代表该工作阶段的一个用户故事（蓝色卡片）或 bug（红色卡片）。可以使用选项卡，将 Teams 看板或你收藏的仪表板直接加入到 Microsoft Teams 中。通过 **选项卡**，团队成员可以在频道或用户个人应用空间中的专用画布上访问你的服务。你可以利用现有 Web 应用在 Teams 中创建优秀的选项卡体验。

1.  在实验室计算机上，切换到显示 Azure DevOps 门户中 **“Tailwind Traders”** 项目的 Web 浏览器，在 Azure DevOps 门户最左侧的垂直菜单栏中单击 **“面板”**，然后并在 **“面板”** 部分单击 **“面板”**。
1.  在 **“面板”** 窗格上的 **“我的团队面板(1)”** 部分，单击 **“Tailwind Traders Team 面板”** 项。
1.  在 **“Tailwind Traders 团队”** 面板上，在 Web 浏览器窗口中，将其 URL 复制到剪贴板。
1.  切换到“Microsoft Teams”窗口，确保选中新创建的团队“**Tailwind Traders**”的“**常规**”频道，并在“**常规**”窗格的上半部分中单击 **“帖子”、“文件”和“Wiki”选项卡** 旁边的加号。这将显示“**添加选项卡**”窗格。
1.  在 **“添加选项卡”** 面板上单击 **“网站”**，在 **“网站”** 面板上将 **“选项卡名称”** 设置为 **“Tailwind Traders 团队面板”**，将 **URL** 设置为你刚才复制到剪贴板的 URL，然后单击 **“保存”**。
1.  在“Microsoft Teams”窗口中，选中“**Tailwind Traders**”团队的“**常规**”频道，在顶部菜单的选项卡列表中，单击新添加的“**Tailwind Traders 团队板**”选项卡，确保其中包含的内容与 Azure DevOps 门户中提供的“**Tailwind Traders 团队**”板一致（可能需要登录）。

> **备注**：可在日站会中监视所有工作，当相应工作项状态更改时，将实时反应更新。还可以从 Microsoft Teams 修改看板。

### 练习 2：集成 Azure Pipelines 与 Microsoft Teams

在此练习中，你将实现 Azure Pipelines 和 Microsoft Teams 之间的集成。

#### 任务 1：在 Microsoft Teams 中安装并配置 Azure Pipelines 应用

在此任务中，你将在 Microsoft Teams 中的指定团队中安装并配置 Azure Pipelines 应用。

> **备注**：通过针对 Microsoft Teams 的 Azure Pipelines 应用，可以监视管道的活动。可以为发布、等待批准和已完成生成等事件设置和管理订阅，将通知直接发布到你的 Teams 频道。还可以从 Teams 频道中批准发布。

1.  转到“Mcrosoft Teams”窗口，单击左下角的“**应用**”图标。这将打开“**应用**”窗格。
1.  在 **“应用”** 窗格上的 **“搜索所有应用”** 文本框中键入 **“Azure Pipelines”**，然后在应用列表中单击 **“Azure Pipelines”**。
1.  在 **Azure Pipelines** 面板上，单击 **“打开”** 按钮右侧的向下箭头，然后在下拉列表中单击 **“添加到团队”** 项。
1.  在 **“为团队设置 Azure Pipelines”** 面板上的 **“搜索”** 文本框中，键入 **“Tailwind Traders”**，在结果列表中选择 **“Tailwind Traders”>“常规”** 项，然后单击 **“设置机器人”**。将自动重定向到 **“Tailwind Traders”** 团队 **“常规”** 频道中的帖子视图。
1.  在“**Tailwind Traders**”团队的“**常规**”频道的帖子列表中，打开“**新对话**”并键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Pipelines**”并按 **Enter** 键，以查看机器人发布的其他消息，如下所示：

    ```
    Here are some of the things you can do:
    subscribe [pipeline url/ project url] - Subscribe to a pipeline or all pipelines in a project to receive notifications
    subscriptions - Add or remove subscriptions for this channel
    feedback - Report a problem or suggest a feature
    signin - Sign in to your Azure Pipelines account
    signout - Sign out from your Azure Pipelines account
    To know more see documentation.
    ```
   
#### 任务 2：在 Microsoft Teams 中订阅 Azure Pipelines 通知

在此任务中，你将在 Microsoft Teams 中订阅 Azure Pipelines 通知

> **备注**：可以使用 `@Azure Pipelines` 句柄开始与该应用交互。

1.  选中“**帖子**”选项卡后，在“**Tailwind Traders**”团队的“**常规**”频道中键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Pipelines**”，然后在命令面板中选择“**登录**”并按 **Enter**。
1.  在 **“Azure Pipelines 登录”** 窗格中，单击 **“登录”**。
1.  如果提示授予 **“服务挂钩(读取和写入)”**、**“生成(生成和执行)”**、**“发布(读取、写入、执行和管理)”**、**“项目和团队(读取)”**、**“标识选取器(读取)”** 和 **“Teams 集成”** 权限，单击 **“接受”**，然后单击 **“关闭”**。

    >**备注**：现在，可以运行 `@azure pipelines subscribe [pipeline url]` 命令以订阅 Azure DevOps 管道。

1.  切换到在 Azure DevOps 门户中显示“**Tailwind Traders**”项目的 Web 浏览器，在 Azure DevOps 门户最左侧的垂直菜单栏中单击“**Pipelines**”，在“**Pipelines**”窗格中单击“**Website-CI**”条目，然后在“**Website-CI**”窗格中的 Web 浏览器窗口中，将其 URL 复制到剪贴板。

    >**备注**：该 URL 的格式为 `https://dev.azure.com/<organization_name>/Tailwind%20Traders/_build?definitionId=<number>`，其中 `<organization_name>` 是代表 DevOps 组织名称的占位符。

    >**备注**：管道 URL 可以指向你的管道中任意页面，只要 URL 中有该管道的 *definitionId* 或 *buildId/releaseId*。

1.  回到“Teams”，在选中“**帖子**”选项卡后，在“**Tailwind Traders**”团队的“**常规**”频道中键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Pipelines**”，然后在命令面板中选择“**订阅**”。此时，粘贴已复制的管道 URL。你的帖子应如下所示：`@Azure Pipelines subscribe https://dev.azure.com/<organization_name>/Tailwind%20Traders/_build?definitionId=<number>`（确保将 `<organization_name>` 占位符替换为你的 DevOps 组织的名称）。按 **Enter**。
1.  等待已成功创建订阅的确认消息。
 
    >**备注**：对于生成管道，频道订阅 **“运行阶段状态更改”** 和 **“运行阶段等待批准”** 通知。

1.  切换到在 Azure DevOps 门户中显示“**Tailwind Traders**”项目的 Web 浏览器，在 Azure DevOps 门户最左侧的垂直菜单栏中单击“**Pipelines**”，在“**Pipelines**”部分中单击“**发布**”，在发布列表中单击“**Website-CD**”条目，在选中“**Website-CD**”条目后，在 Web 浏览器窗口中将其 URL 复制到剪贴板。

    >**备注**：该 URL 的格式将会是 `https://dev.azure.com/<organization_name>/Tailwind%20Traders/_release?_a=releases&view=mine&definitionId=2`，其中 `<organization_name>` 是代表你的 DevOps 组织名称的占位符。

1.  选中“**帖子**”选项卡后，在“**Tailwind Traders**”团队的“**常规**”频道中键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Pipelines**”，然后在命令面板中选择“**订阅**”。此时，粘贴已复制的发布 URL。你的帖子应如下所示：`@Azure Pipelines subscribe https://dev.azure.com/<organization_name>/Tailwind%20Traders/_release?_a=releases&view=mine&definitionId=2`，以订阅发布管道（确保将 `<organization_name>` 占位符替换为你的 DevOps 组织的名称）。按 **Enter**。

    >**备注**：对于发布管道，频道订阅 **“部署开始”**、**“部署完成”** 和 **“部署准等待通知”**。
 
#### 任务 3：使用筛选器自定义 Microsoft Teams 中对 Azure Pipelines 的订阅

在此任务中，你将自定义 Microsoft Teams 中对 Azure Pipelines 的订阅。

>**备注**：当用户订阅任何管道时，会在不应用任何筛选器的情况下默认创建几个订阅。通常，用户需要自定义这些订阅。例如，用户可能希望仅在生成失败或将部署推送到生产环境时获得通知。Azure Pipelines 应用支持通过筛选器自定义频道中显示的内容。

>**备注**：可使用 `@Azure Pipelines subscriptions` 命令列出和管理订阅。此命令会列出该频道的所有当前订阅。

1.  选中“**帖子**”选项卡后，在“**Tailwind Traders**”团队的“**常规**”频道中键入“**@**”，在你键入“**Azure**”时，系统会提示结果，请选择“**Azure Pipelines**”，然后选择“**订阅**”并按 **Enter**。从“**Azure Pipelines**”机器人的回复中，选择“**添加订阅**”。
1.  在 **Azure Pipelines** **“添加订阅”** 面板上的 **“选择事件”** 下拉列表中，确保选择 **“生成完成”** 并单击 **“下一步”**。
1.  在 **Azure Pipelines** **“添加订阅”** 面板上的 **“选择管道”** 下拉列表中，确保选择 **“Website-CI”** 并单击 **“下一步”**。
1.  在 **Azure Pipelines** **“添加订阅”** 面板上的 **“生成状态”** 拉列表中，确保选择 **“[Any]”** 并单击 **“提交”**。
1.  在 **Azure Pipelines** **“添加订阅”** 面板上，单击 **“确定”** 以确认通知消息。
1.  在 **Azure Pipelines** **“查看订阅”** 面板上，查看订阅列表并关闭面板。
1.  切换到在 Azure DevOps 门户中显示“**Tailwind Traders**”项目的 Web 浏览器，在 Azure DevOps 门户最左侧的垂直菜单栏中单击“**Pipelines**”，在“Pipelines”窗格中，单击“**Website-CI**”条目，然后在“Website-CI”窗格中，单击“**运行管道”>“运行**”。 
1. Teams 频道将发布关于管道执行失败的通知，这是预期的行为（管道缺少设置）。


## 回顾

在本实验室中，你实现了 Azure DevOps 服务和 Microsoft Teams 之间的集成方案。
