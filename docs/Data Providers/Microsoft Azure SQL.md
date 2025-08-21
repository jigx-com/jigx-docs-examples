---
title: Microsoft Azure SQL
slug: mCBI-micor
createdAt: Thu Nov 16 2023 18:02:24 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed May 22 2024 07:27:21 GMT+0000 (Coordinated Universal Time)
---

# Microsoft Azure SQL

{% hint style="warning" %}
Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](docId:jrbaNsm-OJn3nf4_dn_Hu) instead. See [REST endpoints from Azure SQL](docId:eOUi2cPYynsdRuK-TobDp) for more information.&#x20;
{% endhint %}

Integrating with an Azure SQL database is easy, using the SQL data provider in Jigx provides access to interact with external data efficiently. For more information on how the the provider functions, see [Microsoft Azure SQL](https://docs.jigx.com/microsoft-azure-sql).

## What is created

In this section, an SQL database is used to create a customer Jigx app that allows you to:

<table><thead><tr><th width="276.41796875">Functions &#x26; Jigs</th><th>Functionality description</th></tr></thead><tbody><tr><td><a href="Microsoft Azure SQL/List customers _SELECT_.md">List customers (SELECT)</a></td><td>View a list of customers.</td></tr><tr><td><a href="Microsoft Azure SQL/List a single customer _SELECT_.md">List a single customer (SELECT)</a></td><td>View a single customer.</td></tr><tr><td><a href="Microsoft Azure SQL/Create a customer _INSERT_.md">Create a customer (INSERT)</a></td><td>Capture new customers in a form.</td></tr><tr><td><a href="Microsoft Azure SQL/Update a customer _UPDATE_.md">Update a customer (UPDATE)</a></td><td>You can update customer details by tapping the Edit customer button. This populates a form with the customer's details and an update button.</td></tr></tbody></table>

## Before you begin

We have simplified the process by providing [database scripts](<Microsoft Azure SQL/Database Scripts.md>) to create the Customer SQL database on which the example is based.

## High-level steps

The SQL data provider is used in Jigx to integrate with an Azure SQL database. In this section, we follow these high-level steps:

1. Identify the SQL database to be used as your data source.
2. Configure SQL connection in Jigx Management.
3. Define a SQL call in a Jigx function in Jigx Builder.
4. Define data operations in the function, such as SELECT, INSERT, UPDATE, and DELETE. For each operation, create a new function to specify the operation.
5. Reference the Jigx functions in jigs.
6. Publish your solution
7. Test the data provider.
