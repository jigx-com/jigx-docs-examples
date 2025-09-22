---
title: sqlite
slug: GLSk-sqlite
createdAt: Thu Jun 09 2022 18:34:04 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 15:06:18 GMT+0000 (Coordinated Universal Time)
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

# sqlite

With SQLite, you can write your datasources as SQL queries. You can use the queries in datasources to create a select statement and get the data from the tables you need to use in your jig file. You can use it directly in the jig file, where the UI component configuration is or you can use it as a global datasource.\
For more information see:

1. [Datasources](https://docs.jigx.com/building-apps-with-jigx/data/datasources)
2. [Datasource SQLite](https://docs.jigx.com/building-apps-with-jigx/data/datasources/sqlite)
3. [SQLite cheatsheet](https://docs.jigx.com/building-apps-with-jigx/data/datasources/sqlite/sqlite-cheatsheet)

## Configuration options

When setting up a SQLite datasource, you use the datasource in the following ways:

1. In your jig file as a locally configured datasource under the `datasource` section.
2. In the global datasource file, that will allow you to use it across all the jig files. The global datasource files are located under the datasources folder in Jigx Builder.

## Examples and code snippets

View common examples of using SQLite below, you can use these as a guideline to configure the same in your solutions.

### sqlite in a jig file

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/Sqlite-employee.png" alt="Locally configured datasource" width="188"><figcaption><p>Locally configured datasource</p></figcaption></figure>
{% endcolumn %}

{% column %}
Datasource with type `sqlite` to select name, and email from the employee's table and to display the list of employees.

**Example**: See the full example on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/simple-lists/dynamic-data/employees-list.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="sqlite-jig" %}
```yaml
datasources:
  employees-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/employees
      query: |
        SELECT
          id,
          '$.firstname',
          '$.email'
        FROM [default/employees]

```
{% endcode %}

### sqlite as a global datasource

{% columns %}
{% column %}
<figure><img src="../../.gitbook/assets/Sqlite-employee.png" alt="Global configured datasource" width="188"><figcaption><p>Global configured datasource</p></figcaption></figure>
{% endcolumn %}

{% column %}
Datasource with type `sqlite` as global datasource to select name, and email from the employee's table and to display the list of employees.

**Example:**\
See the full example on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/simple-lists/dynamic-data/employees-list.jigx)
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="sqlite-global-datasource" %}
```yaml
type: "datasource.sqlite"
options:
    provider: DATA_PROVIDER_DYNAMIC
    entities:
    - entity: default/employees
    query: |
    SELECT
        id,
        '$.firstname',
        '$.email'
    FROM [default/employees]
```
{% endtab %}

{% tab title="list-jig.jigx" %}
```yaml
data: =@ctx.datasources.employees-dynamic
item: 
  type: "component.list-item"
  options:
    title: =@ctx.current.item.firstname
    subtitle: =@ctx.current.item.email
```
{% endtab %}
{% endtabs %}
