
<!---DEFAULT RATE LIMIT-->

{% if include.endpoint=="default" %} 我们将每小时 250,000 个请求的常规 Braze 速率限制应用于此端点，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---PUT /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "update dashboard user" %}
This endpoint has a rate limit of 5000 requests per day. This rate limit is shared with the `/scim/v2/Users/` GET, DELETE, and POST endpoints as they are documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---GET /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "look up dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per one company. This limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---DELETE /scim/v2/Users/YOUR_ID_HERE--->
{% elsif include.endpoint == "delete dashboard user" %}
This endpoint has a rate limit of 5000 requests a day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---POST /scim/v2/Users--->
{% elsif include.endpoint == "create dashboard user" %}
This endpoint has a rate limit of 5000 requests per day, per organization. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and DELETE endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---GET /scim/v2/Users--->
{% elsif include.endpoint == "look up dashboard user email" %}
This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!---/users/external_id/rename-->
<!---/users/external_id/remove-->

{% elsif include.endpoint=="外部 ID 迁移"%} 我们对此端点应用了每分钟 1,000 个请求的速率限制，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/track-->

{% elsif include.endpoint=="用户跟踪" %}我们对所有客户都应用了每分钟50,000个请求的基本速度限制。每个 `/user/track` 请求最多可包含 75 个事件对象、75 个属性对象和 75 个购买对象。每个对象(事件、属性和购买阵列)可以各更新一个用户。总之，这意味着一次呼叫最多可更新 225 个用户。此外，单个用户配置文件可由多个对象更新。

不同的限制适用于已购买**每月活跃用户**的客户 - 24-25 岁。有关这些限制的详细信息，请参阅[每月活跃用户 - 24-25 CY 限制]({{site.baseurl}}/api/endpoints/user_data/post_user_track/#monthly-active-users-cy-24-25)。

请参阅我们的 [API 速率限制]({{site.baseurl}}/api/api_limits/)页面了解详细信息，如果需要增加限制，请与您的客户成功经理联系。

<!---/users/export/ids-->

{% elsif include.endpoint == "用户导出 ID" %} 如果在 2024 年 8 月 22 日或之后使用 Braze 登录，则此端点的速率限制为每分钟 250 个请求，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/delete-->

{% elsif include.endpoint == "用户删除 " % } 对于在 2021 年 9 月 16 日或之后登上 Braze 平台的客户，我们对此端点应用了每分钟 20,000 个请求的共享速率限制。此速率限制与 `/user/alias/new`、`/user/ identify` 和 `/user/merge` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/alias/new-->

{% elsif include.endpoint == "user alias new " % } 对于在 2021 年 9 月 16 日或之后加入 Braze 的客户，我们对此端点应用了每分钟 20,000 个请求的共享速率限制。此速率限制与 `/users/delete`、`/users/ identify`、`/users/merge` 和 `/users/alias/update` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/alias/update-->

{% elsif include.endpoint == "用户别名更新 " % } 对于在 2021 年 9 月 16 日或之后加入 Braze 的客户，我们对此端点应用了每分钟 20,000 个请求的共享速率限制。此速率限制与 `/users/delete`、`/users/ identify`、`/users/merge` 和 `/users/alias/new` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/alias/update-->

{% elsif include.endpoint == "用户别名更新 " % } 对于在 2021 年 9 月 16 日或之后加入 Braze 的客户，我们对此端点应用了每分钟 20,000 个请求的共享速率限制。此速率限制与 `/users/delete`、`/users/ identify` 和 `/users/merge` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/identify-->

{% elsif include.endpoint == "用户标识" %} 对于在 2021 年 9 月 16 日或之后使用 Braze 的客户，我们对此端点应用了每分钟 20,000 个请求的共享速率限制。此速率限制与 `/user/delete`、`/user/alias/new`、`/user/merge` 和 `/user/alias/update` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/users/merge-->

{% elsif include.endpoint == "用户合并 " % } 对于在 2021 年 9 月 16 日或之后加入 Braze 的客户，我们对此端点应用了每分钟 20,000 个请求的共享速率限制。此速率限制与 `/user/delete`、`/user/alias/new`、`/user/ identify` 和 `/user/alias/update` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/custom_attributes-->

{% elsif include.endpoint == "custom\_attributes " % } 对于在 2021 年 9 月 16 日或之后使用 Braze 上机的客户，我们对此端点应用了每小时 1,000 个请求的共享速率限制。此速率限制与 `/events`、`/events/list` 和 `/purchases/product_list` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/events-->

{% elsif include.endpoint == "events " % } 对于在 2021 年 9 月 16 日或之后加入 Braze 的客户，我们对此端点应用了每小时 1,000 个请求的共享速率限制。此速率限制与 `/custom_attributes`、`/events/list` 和 `/purchases/product_list` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/events/list-->

{% elsif include.endpoint == "事件列表 " % } 对于在 2021 年 9 月 16 日或之后使用 Braze 登机的客户，我们对此端点应用了每小时 1,000 个请求的共享速率限制。此速率限制与 `/custom_attributes`、`/events` 和 `/purchases/product_list` 端点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/purchases/product_list-->

{% elsif include.endpoint == "购买产品列表 " % } 对于在 2021 年 9 月 16 日或之后使用 Braze 上机的客户，我们对此端点应用了每小时 1,000 个请求的共享速率限制。此速率限制与 `/custom_attributes`、`/events` 和 `/events/list` 终结点共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/messages/send-->
<!---/campaigns/trigger/send-->
<!---/canvas/trigger/send-->

{% elsif include.endpoint=="发送终结点"%} 在请求中指定段或连接受众时，我们对此终结点应用了每分钟 250 个请求的速率限制。否则，如果指定 `external_id`，此终结点的默认速率限制为每小时 250,000 个请求，这些请求在 `/messages/send`、`/campaigns/trigger/send` 和 `/canvas/trigger/send` 之间共享，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

<!---/transactional/v1/campaigns/{campaign_id}/send -->

{% elsif include.endpoint == "事务性电子邮件" %} 钎焊事务性电子邮件不受速率限制。根据您选择的套餐，SLA 每小时覆盖一组事务性电子邮件。超过该速率的请求仍将发送，但不受 SLA 覆盖。99.9%的电子邮件将在一分钟内发送。

<!---/sends/id/create-->

{% elsif include.endpoint=="sends id create" %} 对于给定的工作区，每天可以通过此端点创建的自定义发送标识符的最大数量为 100。您创建的每个 `send_id` 和 `campaign_id` 组合都将计入您的每日上限。任何有效请求的响应报头都包括当前的速率限制状态，有关详细信息，请参阅 [API 速率限制]({{site.baseurl}}/api/api_limits/)。

<!---/subscription/status/set-->
{% elsif include.endpoint == "subscription status set" %}
This endpoint has a rate limit of 5,000 requests per minute shared across the `/subscription/status/set` and `/v2/subscription/status/set` endpoint as documented in [API rate limits]({{site.baseurl}}/api/api_limits/).

<!-- Add this phrase back ", as documented in [API rate limits]({{site.baseurl}}/api/api_limits/)" to CDI endpoints for GA -->

<!---GET /cdi/integrations--->
{% elsif include.endpoint == "cdi list integrations" %}
This endpoint has a rate limit of 50 requests per minute.

<!---POST /cdi/integrations/{integration_id}/sync--->
{% elsif include.endpoint == "cdi job sync" %}
This endpoint has a limit of 20 requests per minute.

<!---POST /cdi/integrations/{integration_id}/job_sync_status--->
{% elsif include.endpoint == "cdi job sync status" %}
This endpoint has a rate limit of 100 requests per minute.

{% endif %}

<!---Additional if statement for Messaging endpoints-->

{% if include.category == "message endpoints" %}

钎焊端点支持[批处理 API 请求]({{site.baseurl}}/api/api_limits/#batching-api-requests)。对消息传递端点的单个请求可以到达以下任意一个：

- 最多50个特定`的external_id`，每个都有单独的消息参数
- 在 Braze 仪表板中创建的任何大小的段，由其 `segment_id` 指定
- 请求中定义为[连接受众]({{site.baseurl}}/api/objects_filters/connected_audience/)对象的任何大小的受众段

{% endif %}

<!---Additional if statement for /messages/send endpoint-->

{% if include.category == "message send endpoint" %}

钎焊端点支持[批处理 API 请求]({{site.baseurl}}/api/api_limits/#batching-api-requests)。对消息传递端点的单个请求可以到达以下任意一个：

- 最多50个特定`外部_id`
- 在 Braze 仪表板中创建的任何大小的段，由其 `segment_id` 指定
- 请求中定义为[连接受众]({{site.baseurl}}/api/objects_filters/connected_audience/)对象的任何大小的受众段

{% endif %}

{% if include.endpoint == "asynchronous catalog item" %}

此终结点在所有异步目录项终结点之间的共享速率限制为每分钟 16,000 个请求，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

{% endif %}

{% if include.endpoint == "synchronous catalog item" %}

此终结点在所有同步目录项终结点之间的共享速率限制为每分钟 50 个请求，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

{% endif %}

{% if include.endpoint == "synchronous catalog" %}

此终结点在所有同步目录终结点之间的共享速率限制为每分钟 50 个请求，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

{% endif %}

{% if include.endpoint=="异步目录字段"或 include.endpoint=="异步目录选择"%}

此终结点在所有异步目录字段和选择终结点之间的共享速率限制为每分钟 50 个请求，如 [API 速率限制]({{site.baseurl}}/api/api_limits/)中所述。

{% endif %}

{% if include.endpoint == "export campaign analytics" %}

此端点的速率限制为每分钟 50,000 个请求。

{% endif %}
