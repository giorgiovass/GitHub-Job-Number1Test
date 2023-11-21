---
nav_title: API Campaigns
article_title: API Campaigns
page_order: 5
description: "This reference article covers how to generate a campaign_id to include in your API calls and how to configure that campaign."
page_type: reference
tool: Campaigns

---
# Campagnes API

> Cet article de référence explique comment générer une adresse `campaign_id` à inclure dans vos appels API et comment configurer cette campagne.

Les campagnes API sont généralement utilisées pour les messages transactionnels. Lors de la création de campagnes API (et non de [campagnes déclenchées par l'API]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/api_triggered_delivery/)), le tableau de bord Braze n'est utilisé que pour générer une page `campaign_id`, qui vous permet de suivre les analyses pour les rapports de campagne. Vous pouvez également générer un identifiant de variation de message, qui est différent pour chaque variante de votre campagne. 

Vous enverrez ensuite ces informations à votre équipe de développement pour qu'elle les utilise dans la demande d'API, avec :
- Copie de la campagne
- Adhésion du public
- Actifs

Une fois la campagne lancée, vous pouvez consulter les résultats dans le tableau de bord. Les campagnes API utilisent les [API de messagerie de]({{site.baseurl}}/api/endpoints/messaging/) Braze, qui offrent les mêmes options de reporting détaillé et de reciblage que les campagnes créées entièrement via le tableau de bord.

{% alert warning %}
Les campagnes API étant généralement transactionnelles, tous les utilisateurs sont éligibles pour les campagnes API, même ceux qui font partie de votre groupe de contrôle global.
{% endalert %}

## Créer une nouvelle campagne

Allez dans **Messagerie** > **Campagnes** et cliquez sur **Créer une campagne**, puis sélectionnez **Campagnes API**. Vous pouvez maintenant passer à la configuration de votre campagne API.

Une [campagne déclenchée par l'API]({{site.baseurl}}/user_guide/engagement_tools/campaigns/building_campaigns/delivery_types/api_triggered_delivery/) est différente d'une campagne API.

## Configurez votre campagne

Pour configurer votre campagne, procédez comme suit :

1. Ajoutez un titre descriptif pour que vous puissiez trouver les résultats sur notre page de campagnes après avoir envoyé vos messages.
2. Cliquez sur **Ajouter un message** et ajoutez les types de messages qui seront inclus dans votre campagne API. Cela vous permettra de générer un `campaign_id` et un ID de variation de message, qui diffère pour chaque canal que vous incluez. 
3. En option, vous pouvez ajouter un événement de conversion pour suivre les conversions des utilisateurs sur une action spécifique ou un objectif de campagne.
4. Cliquez sur **Enregistrer la campagne** et vous êtes prêt à lancer votre campagne API !

## Appels API

Après avoir sauvegardé votre campagne API, incluez les éléments suivants dans votre demande API : 
- Les champs `campaign_id` générés avec votre demande d'API sont indiqués dans les [points de terminaison d'envoi de messages][2].
- Un [objet message]({{site.baseurl}}/api/objects_filters/#messaging-objects) pour chaque plate-forme incluse dans la campagne. Dans l'objet du message, indiquez l'ID de la variation du message. Cela permet de spécifier que les statistiques doivent être collectées et affichées sous cette variante. Les objets de message suivants sont pris en charge : Android, Content Cards, email, iOS, Kindle, SMS/MMS, web push et webhook.

[2]: {{site.baseurl}}/api/endpoints/messaging/#send-endpoints
