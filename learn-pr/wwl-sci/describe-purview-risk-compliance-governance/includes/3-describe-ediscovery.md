
Electronic discovery, or eDiscovery, is the process of identifying and delivering electronic information that can be used as evidence in legal cases. 

eDiscovery is one of the solutions available through the Microsoft Purview portal, under the Risk & Compliance set of solutions. To access any of the eDiscovery-related tools, a user must be assigned the appropriate permissions.

# [Microsoft Purview portal](#tab/purview-portal)
:::image type="content" source="../media/purview-portal-risk-compliance.png" lightbox="../media/purview-portal-risk-compliance.png" alt-text="A screen capture of the Microsoft Purview portal that highlights eDiscovery in the risk and compliance set of solutions.":::

# [eDiscovery](#tab/ediscovery)
:::image type="content" source="../media/ediscovery-overview.png" lightbox="../media/ediscovery-overview.png" alt-text="A screen capture of the eDiscovery overview page in the Microsoft Purview portal.":::

> [!IMPORTANT]
> eDiscovery can be accessed through the Microsoft Purview compliance portal, but the Microsoft Purview compliance portal is scheduled for retirement by the end of 2024. Unless otherwise stated, information in this unit refers to eDiscovery functionality available through the Microsoft Purview portal.

The Microsoft Purview portal presents a unified UI experience for eDiscovery. If you previously worked with eDiscovery through the Microsoft Purview compliance portal, a key difference is that you'll no longer experience a different UI for eDiscovery (Standard) and eDiscovery (Premium). Instead, you have one consistent UI and depending on the licensing and subscriptions for your organization, you can further manage cases and analyze content using premium eDiscovery features. For example, the images that follow show the UI for an eDiscovery case and how the Review Sets feature is displayed with and without premium features. 

# [Standard features](#tab/standard-features)
:::image type="content" source="../media/ediscovery-standard.png" lightbox="../media/ediscovery-standard.png" alt-text="A screenshot of a case with standard features. Review sets are listed in the UI but not enabled.":::

# [Premium features](#tab/premium-features)
:::image type="content" source="../media/ediscovery-premium.png" lightbox="../media/ediscovery-premium.png" alt-text="A screenshot of a case with premium features. Review sets are listed in the UI and enabled.":::

You can use Microsoft Purview eDiscovery to identify, review, and manage content in Microsoft 365 services to support your investigations. Supported Microsoft 365 services include:

- Exchange Online
- Microsoft Teams
- Microsoft 365 Groups
- OneDrive
- SharePoint
- Viva Engage

The list that follows describes some of the capabilities available with eDiscovery. For a complete listing, refer to the features and capabilities section of the article titled, "Learn about eDiscovery (preview)" linked in the summary and resources unit of this module.

- **Search for content**: Search for content that's stored in Exchange mailboxes, OneDrive accounts, SharePoint sites, Microsoft Teams, Microsoft 365 Groups, and Viva Engage Teams. You can also use keyword queries and search conditions.
- **Search statistics and samples**: After you run a search, you can view statistics of the estimated search results, such as the number and total size of items matching your search criteria. You can also view a representative sample of the items included in the search results.
- **Export search results**: Export search results to a local computer in your organization. When you export search results, items are copied from their original content location and packaged. Then you can download those items in the export package to a local computer.
- **Place content locations on hold**: Preserve content relevant to your investigation by placing a hold on the content locations in a case. Holds let you secure electronically stored information from inadvertent (or intentional) deletion during your investigation.
- **Review sets** (premium feature) -  A review set is a secure, Microsoft-provided Azure Storage location in the Microsoft cloud. When you add data to a review set, the collected items are copied from their original content location to the review set. Review sets provide a static, known set of content that you can search, filter, tag, analyze, and predict relevancy using predictive coding models. You can also track and report on what content gets added to the review set.
- **Advanced indexing** (premium feature) - When a search, review set, or export process is run, the associated content locations where items are partially indexed are reindexed in a process called Advanced indexing. Advanced indexing ensures any content deemed as partially indexed is reprocessed to make it fully searchable when you collect data for an investigation.
- **Optical character recognition (OCR)** (premium feature) - When content is added to a review set, OCR functionality extracts text from images, and includes the image text with the content that's added to a review set. This lets you search for image text when you query the content in the review set.
- **Conversation threading** (premium feature) - When chat messages from Teams and Viva Engage conversations are added to a review set, you can collect the entire conversation thread. The entire chat conversation that contains items that match the search criteria is added to the review set. This lets you review chat items in the context of the back-and-forth conversation.
- **Analytics** (premium feature) - eDiscovery allows you to analyze review set documents to help you organize the documents in a coherent manner and reduce the volume of documents to be reviewed. Near duplicate detection groups textually similar documents together to help you make your review process more efficient. Email threading identifies specific email messages that give a complete context of the conversation in an email thread. Themes functionality attempts to analyze themes in review set documents and assign a theme to documents so that you can review documents with related theme. These analytics capabilities help make your review process more efficient so that reviewers can review a fraction of collected documents.

### Integration with Microsoft Copilot for Security

Microsoft Purview eDiscovery supports integration with Microsoft Copilot for Security, through the embedded experience. Users whose organization has been onboarded to Copilot, have enabled Copilot to access data from Microsoft 365 services, and have the appropriate role permissions can experience Copilot integration through the following supported capabilities:

- Gain contextual summary of evidence collected in eDiscovery review sets (Preview).
- Natural language to keyword query language (keyQL) queries.

#### Gain contextual summary of evidence collected in eDiscovery review sets (Preview).
eDiscovery admins or managers spend a significant amount of time reviewing evidence collected in review sets. You can use Copilot for Security in Microsoft Purview to provide a contextual summary of most items in a review set.

The summary provided is in the context of text included in a selected item. This summary can save time for reviewers by quickly identifying information helpful when tagging or exporting items.

Copilot for Security summarizes the entire item, including documents, meetings transcripts, or attachments. You can also ask follow-up contextual questions about the summary.

:::image type="content" source="../media/purview-ediscovery-context-v2.png" lightbox="../media/purview-ediscovery-context-v2.png" alt-text="Screen capture of the context generated by Copilot for an item in a review set of Microsoft Purview eDiscovery (Premium).":::

#### Natural language to KeyQL queries

With Copilot integration in eDiscovery, eDiscovery managers can use natural language prompts to generate keyQL queries. With the query generated, you can save it or run the query. Copilot also provides prompt suggestions that can be generated into a query.

:::image type="content" source="../media/ediscovery-copilot-keyword-query.png" lightbox="../media/ediscovery-copilot-keyword-query.png" alt-text="Screen capture showing the user interface for drafting a query with Copilot, using natural language. The option to use available prompts to generate the query is also shown.":::
