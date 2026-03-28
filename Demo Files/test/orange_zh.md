---
nav\_title:邮递员和其他请求文章\_标题：邮递员和其他要求 page\_order:3\. 说明："这篇参考文章涵盖了铜邮差收藏，它的作用，如何设置和使用收藏，以及如何编辑和发送所有请求 。 " page\_type: reference

---

# 邮递员和其他样品要求

> Braze 允许您通过我们的邮递员集合生成我们端点的测试 API 请求。本参考文章介绍了铜邮差收藏，它是什么，如何设置和使用收藏，以及如何编辑和发送请求。

## 什么是邮递员？ What is Postman?

Postman 绝对是构建 API 请求的免费使用的可视化编辑工具。与其他与 API 交互的方法(例如，使用 cURL)不同，Postman 允许您轻松编辑 API 请求、查看头信息等等。Postman 允许您保存预先制作的 API 请求样本的收藏或库。为了让我们的客户能够轻松启动并运行我们的REST API,我们为所有API端点创建了一个带有预制示例的集合。

在[邮递员文档](https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#intro)中单击**运行邮递员**以开始，查看或下载我们的邮递员收藏。

## 使用布拉兹邮递员系列

如果您拥有邮递员帐户(并且您可以从[邮递员网站][1]下载相应的macOS、Windows和Linux版本 ) , 您可以通过点击橙色的**Run in Postman**按钮在自己的邮递员应用程序中打开我们的邮递员文档。然后，您可以[创建环境](#setting-up-your-postman-environment)，或使用我们的 Braze REST API 环境作为模板，编辑可用的 `POST` 和 `GET` 请求以满足您的需求。

### 设置邮递员环境

{% raw %} Braze Postman Collection 使用模板变量 `{instance_url}` 将 Braze 实例的 REST API URL 替换为预构建的请求，并使用 `{api_key}` 变量替换为 API Key。您不必手动编辑收藏中的所有请求，而是可以在邮递员环境中设置此变量。您可以从下拉列表中选择我们的模板化环境(Braze REST API 环境模板)并将变量值替换为自己的，也可以设置自己的环境。{% endraw %}

要设置自己的环境，请执行以下步骤：

1. "从""**工作区"**"选项卡中，选择""**环境**"" 。"
2. 单击**+**+按钮以创建新环境。
3. 给这个环境一个名称（例如“Braze API Requests”），并为`instance_url`和`api_key`添加键，键值对应于你的\[Braze instance]\[7]和\[Braze REST API Key]\[8]。
4. 单击**保存**。

{% alert note %} 在`POST`请求正文中，`api_key` 应该封装在引号中：`"MY-API-KEY-EXAMPLELE"`.在 `GET` URL 中，不应该是。我们已经在本文档的`帖子`请求正文、`GET` URL 和 `YOUR-API-KEY-HERE` 的环境模板中为您提供了此格式。{% endalert %}

\![在 Postman 中的 Braze REST API 环境中添加 API 密钥和实例 URL 的变量。]\[3]

### 使用集合中的预构建请求

配置环境后，可以使用集合中的任何预构建请求作为构建新 API 请求的模板。要开始使用某个预建请求，请在邮递员的**"收藏"**菜单中单击它。这将在邮递员应用程序主窗口中以新选项卡的形式打开请求。

一般来说，Braze API 端点接受的请求有两种类型 - `GET` 和 `POST`。根据端点使用哪种 `HTTP` 方法，您需要以不同方式编辑预构建的请求。

#### 编辑 POST 请求

编辑`POST`请求时，打开请求并转到请求编辑器中的**正文**部分。为可读性，选择**原始单**选按钮以格式化 `JSON` 请求正文。

\![在邮递员中编辑 POST 用户跟踪请求时的正文选项卡]\[4]

#### 编辑 GET 请求

编辑 `GET` 请求时，编辑请求 URL 中传递的参数。为此，请选择"**参数"**选项卡，并在出现的字段中编辑键值对，以使其正常工作。

\![在 Postman 中编辑未订阅电子邮件地址请求的 GET 查询列表时的参数选项卡。]\[5]

### 发送您的请求

准备好 API 请求后，单击**发送**。请求发送，响应数据填充在请求编辑器下方的部分。从这里，您可以查看从 Braze API 返回的原始数据，查看 HTTP 响应代码，查看请求处理的时间，以及查看头信息。

\![状态为 201 已创建，响应时间为 269 毫秒的 POST 请求中的正文响应数据示例。]\[6]

[1]: https://www.getpostman.com
\[3]: {% image\_buster /assets/img\_archive/postman\_variable.png %} \[4]: {% image\_buster /assets/img\_archive/postman\_post.png %} \[5]: {% image\_buster /assets/img\_archive/postman\_get.png %} \[6]: {% image\_buster /assets/img\_archive/postman\_response.png %} \[7]: {{{site.baseurl}/developer\_guide/rest\_api/basics/#endpoints \[8]: {{site.baseurl}/api\_key/
