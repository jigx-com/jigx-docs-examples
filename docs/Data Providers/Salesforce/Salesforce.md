---
title: Salesforce
slug: X2PD-sa
createdAt: Thu Nov 16 2023 18:04:02 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 28 2023 05:02:23 GMT+0000 (Coordinated Universal Time)
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Salesforce

Jigx easily integrates with your Salesforce instance, through the [Salesforce data provider](https://docs.jigx.com/building-apps-with-jigx/data/data-providers/salesforce). The following examples with code snippets are provided in this section:

* [Create records in objects](<Create records in objects.md>)
* [Delete records in objects](<Delete records in objects.md>)
* [Save & update records in objects](<Save _ update records in objects.md>)
* [List records in objects](<List records in objects.md>)

Creating a Salesforce dashboard can help you gain valuable insight into your business, improve decision-making, and enhance overall efficiency and performance across your organization. The Jigx Salesforce provider brings data directly into the app from Salesforce, giving you access to real-time data and visual insights no matter where you are. Tailor the app to display metrics that matter most to your business and configure them to suit different user roles and responsibilities. Dashboards can be shared with team members, managers, or stakeholders. Sales teams can benefit significantly from Salesforce dashboards as they provide a clear view of their pipelines, opportunities, and sales targets.

{% embed url="https://vimeo.com/846066533" %}

{% hint style="warning" %}
Examples are based on test data in a Jigx demo Salesforce environment. Copying the sample code must be adjusted to represent your own Salesforce environment.
{% endhint %}

{% columns %}
{% column %}
<figure><img src="../../../.gitbook/assets/SalesFDashboard.PNG" alt="Salesforce Dashboard" width="188"><figcaption><p>Salesforce Dashboard</p></figcaption></figure>
{% endcolumn %}

{% column %}
In this dashboard the Home Hub is configured to call eight jigs and one datasource file. The jigs use various components such as [form](../../Components/form/form.md), [list](../../Components/list/list.md), [widgets](https://docs.jigx.com/examples/readme/widgets), [bar-chart](../../Components/charts/bar-chart.md), and actions to create an informative interactive app. The Salesforce provider references various Salesforce objects as shown below.
{% endcolumn %}
{% endcolumns %}

{% code title="salesforce data provider" %}
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
{% endcode %}
