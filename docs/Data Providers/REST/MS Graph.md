---
title: MS Graph
slug: Qayy-m
createdAt: Tue Apr 30 2024 08:12:15 GMT+0000 (Coordinated Universal Time)
updatedAt: Mon May 06 2024 07:39:19 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The [MS Graph](https://docs.jigx.com/microsoft-graph-oauth) examples below use the User, Calendar, Mail, Insights, and To-do tasks resource types to create a powerful Jigx apps with everything you need in one app. The REST data provider requires you to [configure OAuth for MS Graph](https://docs.jigx.com/configuring-oauth-for-ms-graph) and the accessToken is used in the Jigx function.

:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/uOotaEt1EWiXLQU0lzxGr_msgraph.gif" size="70" position="center"}
:::
::::

:::hint{type="success"}
When using the code and samples in this topic, remember that they are designed to function as part of a comprehensive solution. To fully benefit from the intended functionality and ensure compatibility, it is recommended that you use the entire solution rather than selecting individual components in isolation. Alternatively, you can use these samples as a guide to understand the underlying concepts and MS Graph API, which can help you integrate similar solutions into your projects more effectively. The entire MS Graph solution is available on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-MS-Graph-demonstrator).
:::

The following examples and code snippets are provided:

|                                                          |                                                                                                                                                                                                                               |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Graph User Profile](<./MS Graph/Graph User Profile.md>) | Provides sample code to get a user's profile information from Microsoft Graph. It includes a [code sample](<./MS Graph/Graph User Profile/Update Profile Photo.md>) for updating a user's profile picture in Microsoft Graph. |
| [Graph Calendar](<./MS Graph/Graph Calendar.md>)         | Provides sample code to get a list of the user's calendars and renders a calendar in a schedule view on a jig. It includes a code sample on adding calendar entries to a user's Microsoft 365 calendar in Exchange.           |
| [Graph Mail](<./MS Graph/Graph Mail.md>)                 | Provides sample code to get a list of emails for a user and displays the emails in a list jig. Press on an email to view the content of the email.                                                                            |
| [Graph tasks](<./MS Graph/Graph tasks.md>)               | Provides sample code to get a list of To-do tasks for a user and displays the tasks in a list jig.                                                                                                                            |
| [Graph Insights](<./MS Graph/Graph Insights.md>)         | provides sample code to get insights that include a list of documents trending around the user and displays the list in a list jig.                                                                                           |
