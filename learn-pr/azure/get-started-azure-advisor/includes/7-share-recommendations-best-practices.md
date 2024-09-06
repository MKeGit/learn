Now let's look at some ways you can manage your Advisor recommendations to more easily apply the documented best practices we've learned about so far.

Let's say you've gone through Advisor and either resolved, postponed, or dismissed all of your recommendations. Now what do you do?

Well, in addition to regularly checking your Advisor dashboard to see your Advisor Score and  recommendations, you can also set up alerts and recommendation digests to help you manage your Advisor process.

- **Alerts** inform you when you have new recommendations to investigate.
- **Recommendation digests** periodically send you a summary of your active recommendations.

## Advisor alerts

You can configure Azure Advisor to send you an alert whenever a new recommendation is available for one of your resources. You choose a subscription and optionally a resource group, and Advisor alerts notifies you of recommendations for those resources.

You can also further specify your alerts by choosing from the following properties:

- Category
- Impact level
- Recommendation type

> [!NOTE]
> Advisor alerts are currently not supported for **Security** recommendations.

### How do I set up alerts?

You can set up alerts from the Advisor dashboard by first selecting **Alerts (Preview)** from the left panel.

:::image type="content" source="../media/azure-advisor-alerts-select.png" alt-text="Screenshot showing how to open the Alerts page." lightbox="../media/azure-advisor-alerts-select.png":::

On the **Advisor - Alerts** page that opens, select **New Advisor Alert** to start creating a new alert. Or, if you already have alerts set up, you can select one to edit.

:::image type="content" source="../media/azure-advisor-alerts-new-alert.png" alt-text="Screenshot showing how to create a new Advisor alert." lightbox="../media/azure-advisor-alerts-new-alert.png":::

When creating or editing an alert, specify the following configurations:

- **SCOPE:** Select the subscription and (optionally) the resource group for which you want to receive an alert.
- **CONDITION:** Choose a specific category, impact level, or recommendation type for the alert.
- **ACTION GROUPS:** Select an existing action group or create a new one to define the list of notifications that are sent when an alert is triggered, such as through email or SMS.
- **ALERT DETAILS:** Provide a name and description for the alert. You can also choose to have the alert enabled or disabled when you save your changes.

That's it! Once you configure and save the alert, you're notified whenever a new recommendation that matches those settings is available.

## Recommendation digests

Another useful tool in managing your Advisor recommendations is through recommendation digests. This feature lets you configure periodic notifications that summarize all your active recommendations across different categories. Similar to Advisor alerts, you can choose how you want to be notified, such as through email, SMS or action groups.

### How do I set up a recommendation digest?

You can set up a recommendation digest from the Advisor dashboard by first selecting **Recommendation digests** from the left panel.

:::image type="content" source="../media/azure-advisor-recommendation-digest-select.png" alt-text="Screenshot showing how to open the recommendation digest page." lightbox="../media/azure-advisor-recommendation-digest-select.png":::

In the **Advisor - Recommendation digests** page that opens, select **New Recommendation Digest** to start creating a new recommendation digest. Ff you already have one set up, you can select it to edit.

Specify similar configurations as you did for Advisor Alerts:

- **SCOPE:** Select the subscription for which you want to receive recommendation digest notifications.
- **CONDITION:** Specify how often you're notified, which categories you want to include, and in what language you want to receive the recommendation digest.
- **ACTION GROUPS:** Select an existing action group or create a new one to define the list of notifications that are sent for the recommendation digest, such as through email or SMS.
- **DIGEST DETAILS:** Provide a name for the recommendation digest. You can also choose to enable or disable it when you save your changes.

:::image type="content" source="../media/azure-advisor-recommendation-digest.png" alt-text="Screenshot showing the Add and Advisor recommendation digest page." lightbox="../media/azure-advisor-recommendation-digest.png":::

After you've configured and saved the recommendation digest, you'll receive your notification as often as you indicated. The recommendation digest provides a summary of all your active recommendations across the different categories you specified.

## Export Advisor reports

Remediating Advisor-surfaced issues often has to be a "team sport." Multiple people and groups must be involved to review, approve, and act on Advisor recommendations.

Advisor helps by letting you download a summary of your recommendations as either a PDF or CSV file. In this way, you can easily share Advisor findings with your colleagues or perform your own analysis on the recommendation data.

From the Advisor dashboard, select **Download as CSV** or **Download as PDF** on the action bar.

:::image type="content" source="../media/azure-advisor-export-recommendations.png" alt-text="Screenshot showing how to export Advisor recommendations." lightbox="../media/azure-advisor-export-recommendations.png":::

The downloaded file includes any filters you applied to the Advisor dashboard. In addition, if you select the Download option while viewing a specific recommendation category or recommendation, the downloaded summary only includes information for that category or recommendation.

## API

As with many features in Azure, a REST API is also available to help you manage most of the things you've learned about Azure Advisor. For example, enterprises use our API to manage recommendations at scale by integrating with their existing work management systems.

For more information, see [Azure Advisor REST API](/rest/api/advisor/?azure-portal=true).
