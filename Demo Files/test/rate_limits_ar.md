
<!---DEFAULT RATE LIMIT-->

{% if include.endpoint == "default" %} نقوم بتطبيق حد معدل Braze العادي البالغ 250,000 طلب في الساعة على نقطة النهاية هذه، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

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

{% elsif include.endpoint == "external id migration" %} نقوم بتطبيق حد معدل يبلغ 1000 طلب في الدقيقة على نقطة النهاية هذه، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/track-->

{% elsif include.endpoint == "users track" %} نقوم بتطبيق حد سرعة أساسي قدره 50000 طلب في الدقيقة على نقطة النهاية هذه لجميع العملاء. يمكن أن يحتوي كل طلب `/users/track` على ما يصل إلى 75 كائن حدث، و75 كائن سمة، و75 كائن شراء. يمكن لكل عنصر (مصفوفات الأحداث والسمات والمشتريات) تحديث مستخدم واحد فقط. وهذا يعني أنه يمكن تحديث 225 مستخدمًا كحد أقصى في مكالمة واحدة. بالإضافة إلى ذلك، يمكن تحديث ملف تعريف المستخدم الواحد بواسطة عدة عناصر.

تُطبق حدود مختلفة على العملاء الذين اشتروا **باقة المستخدمين النشطين شهريًا - السنة المالية 24-25** . للاطلاع على تفاصيل هذه الحدود، راجع [حدود المستخدمين النشطين شهريًا - حدود السنة 24-25]({{site.baseurl}}/api/endpoints/user_data/post_user_track/#monthly-active-users-cy-24-25) .

راجع صفحتنا حول [حدود معدل API]({{site.baseurl}}/api/api_limits/) للحصول على التفاصيل، وتواصل مع مدير نجاح العملاء الخاص بك إذا كنت بحاجة إلى زيادة الحد المسموح به.

<!---/users/export/ids-->

{% elsif include.endpoint == "users export ids" %} إذا قمت بالتسجيل في Braze في أو بعد 22 أغسطس 2024، فإن نقطة النهاية هذه لها حد معدل يبلغ 250 طلبًا في الدقيقة، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/delete-->

{% elsif include.endpoint == "users delete" %} بالنسبة للعملاء الذين انضموا إلى منصة Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 20000 طلب في الدقيقة لنقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/users/alias/new` و `/users/identify` و `/users/merge` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/alias/new-->

{% elsif include.endpoint == "users alias new" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 20000 طلب في الدقيقة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/users/delete` و `/users/identify` و `/users/merge` و `/users/alias/update` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/alias/update-->

{% elsif include.endpoint == "users alias update" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 20000 طلب في الدقيقة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/users/delete` و `/users/identify` و `/users/merge` و `/users/alias/new` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/alias/update-->

{% elsif include.endpoint == "users alias update" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 20000 طلب في الدقيقة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/users/delete` و `/users/identify` و `/users/merge` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/identify-->

{% elsif include.endpoint == "users identify" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 20000 طلب في الدقيقة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/users/delete` و `/users/alias/new` و `/users/merge` و `/users/alias/update` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/users/merge-->

{% elsif include.endpoint == "users merge" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 20000 طلب في الدقيقة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/users/delete` و `/users/alias/new` و `/users/identify` و `/users/alias/update` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/custom_attributes-->

{% elsif include.endpoint == "custom\_attributes" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 1000 طلب في الساعة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/events` و `/events/list` و `/purchases/product_list` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/events-->

{% elsif include.endpoint == "events" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 1000 طلب في الساعة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/custom_attributes` و `/events/list` و `/purchases/product_list` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/events/list-->

{% elsif include.endpoint == "events list" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 1000 طلب في الساعة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/custom_attributes` و `/events` و `/purchases/product_list` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/purchases/product_list-->

{% elsif include.endpoint == "purchases product list" %} بالنسبة للعملاء الذين انضموا إلى Braze في أو بعد 16 سبتمبر 2021، فإننا نطبق حدًا مشتركًا لمعدل الطلبات يبلغ 1000 طلب في الساعة على نقطة النهاية هذه. يتم مشاركة حد المعدل هذا مع نقاط النهاية `/custom_attributes` و `/events` و `/events/list` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/messages/send-->
<!---/campaigns/trigger/send-->
<!---/canvas/trigger/send-->

{% elsif include.endpoint == "send endpoints" %} عند تحديد شريحة أو جمهور متصل في الطلب، نقوم بتطبيق حد معدل يبلغ 250 طلبًا في الدقيقة على نقطة النهاية هذه. بخلاف ذلك، إذا تم تحديد `external_id` ، فإن نقطة النهاية هذه لها حد معدل افتراضي يبلغ 250,000 طلب في الساعة يتم مشاركته بين `/messages/send` و `/campaigns/trigger/send` و `/canvas/trigger/send` ، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

<!---/transactional/v1/campaigns/{campaign_id}/send -->

{% elsif include.endpoint == "transactional email" %} لا تخضع رسائل البريد الإلكتروني الخاصة بالمعاملات من Braze لحدود المعدل. بحسب الباقة التي اخترتها، يتم تغطية عدد محدد من رسائل البريد الإلكتروني الخاصة بالمعاملات في الساعة الواحدة بموجب اتفاقية مستوى الخدمة (SLA). الطلبات التي تتجاوز هذا المعدل ستظل تُرسل، ولكنها غير مشمولة باتفاقية مستوى الخدمة. 99.9% من رسائل البريد الإلكتروني سترسل في أقل من دقيقة واحدة.

<!---/sends/id/create-->

{% elsif include.endpoint == "sends id create" %} الحد الأقصى اليومي لعدد معرّفات الإرسال المخصصة التي يمكن إنشاؤها عبر نقطة النهاية هذه هو 100 لمساحة عمل معينة. سيتم احتساب كل مجموعة `من send_id` و `campaign_id` تقوم بإنشائها ضمن الحد اليومي المسموح به. تتضمن رؤوس الاستجابة لأي طلب صالح حالة حد المعدل الحالي، راجع [حدود معدل واجهة برمجة التطبيقات]({{site.baseurl}}/api/api_limits/) لمزيد من التفاصيل.

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

تدعم نقاط نهاية Braze [تجميع طلبات واجهة برمجة التطبيقات (API)]({{site.baseurl}}/api/api_limits/#batching-api-requests) . يمكن لطلب واحد إلى نقاط نهاية المراسلة أن يصل إلى أي مما يلي:

- ما يصل إلى 50 `معرّفًا خارجيًا` محددًا، لكل منها معلمات رسالة فردية
- شريحة من أي حجم يتم إنشاؤها في لوحة تحكم Braze، ويتم تحديدها بواسطة `segment_id` الخاص بها
- شريحة جمهور بأي حجم، محددة في الطلب ككائن [جمهور متصل]({{site.baseurl}}/api/objects_filters/connected_audience/)

{% endif %}

<!---Additional if statement for /messages/send endpoint-->

{% if include.category == "message send endpoint" %}

تدعم نقاط نهاية Braze [تجميع طلبات واجهة برمجة التطبيقات (API)]({{site.baseurl}}/api/api_limits/#batching-api-requests) . يمكن لطلب واحد إلى نقاط نهاية المراسلة أن يصل إلى أي مما يلي:

- ما يصل إلى 50 `معرفًا خارجيًا` محددًا
- شريحة من أي حجم يتم إنشاؤها في لوحة تحكم Braze، ويتم تحديدها بواسطة `segment_id` الخاص بها
- شريحة جمهور بأي حجم، محددة في الطلب ككائن [جمهور متصل]({{site.baseurl}}/api/objects_filters/connected_audience/)

{% endif %}

{% if include.endpoint == "asynchronous catalog item" %}

تحتوي نقطة النهاية هذه على حد معدل مشترك يبلغ 16000 طلب في الدقيقة بين جميع نقاط نهاية عناصر الكتالوج غير المتزامنة، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

{% endif %}

{% if include.endpoint == "synchronous catalog item" %}

تحتوي نقطة النهاية هذه على حد معدل مشترك يبلغ 50 طلبًا في الدقيقة بين جميع نقاط نهاية عناصر الكتالوج المتزامنة، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

{% endif %}

{% if include.endpoint == "synchronous catalog" %}

تحتوي نقطة النهاية هذه على حد معدل مشترك يبلغ 50 طلبًا في الدقيقة بين جميع نقاط نهاية الكتالوج المتزامنة، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

{% endif %}

{% if include.endpoint == "asynchronous catalog fields" or include.endpoint == "asynchronous catalog selections" %}

تحتوي نقطة النهاية هذه على حد معدل مشترك يبلغ 50 طلبًا في الدقيقة بين جميع نقاط نهاية حقول الكتالوج غير المتزامنة ونقاط نهاية التحديد، كما هو موثق في [حدود معدل API]({{site.baseurl}}/api/api_limits/) .

{% endif %}

{% if include.endpoint == "export campaign analytics" %}

يبلغ الحد الأقصى لمعدل الطلبات لهذه النقطة النهائية 50000 طلب في الدقيقة.

{% endif %}
