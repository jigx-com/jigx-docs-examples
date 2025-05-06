---
title: Salesforce
slug: X2PD-sa
createdAt: Thu Nov 16 2023 18:04:02 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 28 2023 05:02:23 GMT+0000 (Coordinated Universal Time)
---

Jigx easily integrates with your Salesforce instance,  through the [Salesforce data provider](). The following examples with code snippets are provided in this section:

- [Create records in objects](<./Salesforce/Create records in objects.md>)
- [Delete records in objects](<./Salesforce/Delete records in objects.md>)
- [Save & update records in objects](<./Salesforce/Save _ update records in objects.md>)
- [List records in objects](<./Salesforce/List records in objects.md>)

Creating a Salesforce dashboard can help you gain valuable insight into your business, improve decision-making, and enhance overall efficiency and performance across your organization. The Jigx Salesforce provider brings data directly into the app from Salesforce, giving you access to real-time data and visual insights no matter where you are.  Tailor the app to display metrics that matter most to your business and configure them to suit different user roles and responsibilities. Dashboards can be shared with team members, managers, or stakeholders. Sales teams can benefit significantly from Salesforce dashboards as they provide a clear view of their pipelines, opportunities, and sales targets.&#x20;

::embed[]{url="https://vimeo.com/846066533"}

:::hint{type="warning"}
Examples are based on test data in a Jigx demo Salesforce environment. Copying the sample code must be adjusted to represent your own Salesforce environment.&#x20;
:::

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/HVVwC60g4xu-W3wdJBW8O_salesfdashboard.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/HVVwC60g4xu-W3wdJBW8O_salesfdashboard.PNG" size="98" width="1240" height="2500" position="center" caption="Salesforce Dashboard" alt="Salesforce Dashboard"}
:::

:::VerticalSplitItem
In this dashboard the Home Hub is configured to call eight jigs and one datasource file. The jigs use various components such as [form](./../Components/form.md), [list](./../Components/list.md), [widgets](), [bar-chart](./../Components/charts/bar-chart.md), and actions to create an informative interactive app.&#x20;

The Salesforce provider references various Salesforce objects as shown below.

```yaml
provider: DATA_PROVIDER_SALESFORCE
entities:
  - Account
  - Opportunity
  - OpportunityStage
  - User
  - UserRole
  - Territory2
```


:::
::::

