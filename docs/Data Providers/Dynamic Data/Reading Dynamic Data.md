---
title: Reading Dynamic Data
slug: KNt_-reading-dynamic-data-tables
description: Learn how to display employee data on a mobile device using Jigx. This document covers creating a Jig to list employees, configuring the YAML for data source and query, customizing list item display, publishing the solution, and includes a helpful screens
createdAt: Wed Jul 13 2022 10:22:47 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Mar 06 2025 08:38:51 GMT+0000 (Coordinated Universal Time)
---

In this example, we **read** the employee data records we created in the employee Dynamic Data table ([Creating Dynamic Data](<./Creating Dynamic Data.md>)), to create a list of the employees and their details.

## Datasources, jig & component

1. **default.jigx** is the database where the Dynamic Data table is defined.
2. [sqlite](./../../Datasource/sqlite.md) datasource calls the Dynamic Data provider, using an SQL query to return the data.
3. [jig.list](<./../../Jig Types/jig_list.md>) is the type of jig we will use to list the data.
4. [expander](./../../Components/expander.md) component to show the Dynamic Data in.

## Examples and code snippets

This example uses the Dynamic Data table, columns, and data records created in the [Creating Dynamic Data](<./Creating Dynamic Data.md>) example to create a list of employees with their details.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-INvHFGW3XIisjDMFXvQ_a-20250306-083847.png" size="78" position="center" caption="Reading Dynamic Data " alt="Reading Dynamic Data "}

Here is what the data table employee resembles in [Data]() in Jigx Management.

![Employee Dynamic Data](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ryCmLjukF38TWd_rs1Ayw_dd-list-mngt.png "Employee Dynamic Data")

:::CodeblockTabs
list-employees.jigx

```yaml
title: Employee list
type: jig.list
icon: list-stars

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1531545514256-b1400bc00f31?q=80&w=1374&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# Use onfocus action to sync the data from the provider everytime the jig is opened  
onFocus:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        options:
        # The dynamic provider has the employee table and records that must sync when the jig is opened
          provider: DATA_PROVIDER_DYNAMIC
          entities:
            - default/employee

datasources:
  my-employees:
  # Use the SQLite data source to write a select query to return the exact data from the solution's Dynamic Data employee table to be used in the jig 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/employee
  
      query: SELECT
               id,
               '$.first_name',
               '$.last_name', 
               '$.job_title',
               '$.email',
               '$.start_date',
               '$.department',
               '$.contact'
              FROM
               [default/employee] 

# Reference the datasource above to use as the data in the expander component
data: =@ctx.datasources.my-employees
item:
  type: component.expander
  options:
    header:
      centerElement: 
        type: component.titles
        options:
        # expressions are used to combine data from two columns to show in the list
          title: =(@ctx.current.item.first_name & ' ' & @ctx.current.item.last_name)
          subtitle: =@ctx.current.item.job_title
          icon: person
          
    children:
      - type: component.entity
        options:
          children:
            - type: component.entity-field
              options:
                label: Position
                value: =@ctx.current.item.job_title
            - type: component.entity-field
              options:
                label: Department
                value: =@ctx.current.item.department
            - type: component.entity-field
              options:
                label: Contact
                value: =@ctx.current.item.contact
                contentType: phone
            - type: component.entity-field
              options:
                label: Email
                value: =@ctx.current.item.email
                contentType: email

```

default.jigx

```yaml
tables:
  employee: null
```

index.jigx

```yaml
ame: employees
title: Employees
category: business

tabs:
  home:
    jigId: list-employees
    icon: home-apps-logo
```
:::

