---
lab:
    title: '实验室：验证实验室环境'
    module: '模块 0：欢迎'
---

# 实验室：验证实验室环境
# 学生实验室手册

## 说明

1. 从讲师或其他来源获取新的 Azure Pass 促销代码（有效期为 30 天）。
2. 使用专用浏览器会话在 account.microsoft.com 获取新的 Microsoft 帐户 (MSA)，或者使用现有帐户。
3. 使用该浏览器会话转到 Microsoftazurepass.com，使用 Microsoft 帐户 (MSA) 兑换 Azure Pass。[兑换 Microsoft Azure Pass](https://www.microsoftazurepass.com/Home/HowTo?Length=5) 请按照说明进行兑换。 
4. 使用该浏览器会话转到 portal.azure.com，然后搜索“Azure DevOps”。在出现的页面中，单击“Azure DevOps 组织”。 
5. 接下来，单击名为“我的 Azure DevOps 组织”的链接（或导航到 https://aex.dev.azure.com/）。
6. 在左侧下拉框中，选择“默认”，而不是“Microsoft 帐户”。
7. 使用默认目录创建新的组织（在屏幕的右上角找到蓝色框）。 
8. 选择新创建的组织，然后在屏幕左侧选择“组织设置”。
9. 导航到“组织设置”->“计费”->“设置计费”->选择一个 Azure 订阅，然后依次选择 zure Pass 订阅和“MS 托管的 CI/CD”，再将“付费并行作业”字段设置为 1。然后在底部的蓝色框中单击“保存”。 
10. 至少要等待 3 个小时才能使用 CI/CD 功能，以便新设置反映在后端中。否则，仍会显示消息“此代理未运行，因为已达到最大请求数量…”。
11. （可选）若要验证这一点，可通过启用了计费的新创建的组织在 https://azuredevopsdemogenerator.azurewebsites.net/ 中创建新的预定义项目。请等待一段时间，然后再运行测试生成。
