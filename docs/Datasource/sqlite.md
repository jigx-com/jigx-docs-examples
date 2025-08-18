---
title: sqlite
slug: GLSk-sqlite
createdAt: Thu Jun 09 2022 18:34:04 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 15:06:18 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn how to utilize SQLite as a datasource in Jig files with this
  comprehensive guide. Discover how to retrieve data through SQLite queries,
  configure it as a local or global datasource, and seamless
---

# sqlite

With SQLite, you can write your datasources as SQL queries. You can use the queries in datasources to create a select statement and get the data from the tables you need to use in your jig file. You can use it directly in the jig file, where the UI component configuration is or you can use it as a global datasource.

{% hint style="info" %}
If you are not familiar with datasources yet, see the [data](https://docs.jigx.com/aI2F-data) section.
{% endhint %}

### Configuration options

When setting up a SQLite datasource, you use the datasource in the following ways:

1. In your jig file as a locally configured datasource under the `datasource` section.
2. In the global datasource file, that will allow you to use it across all the jig files. The global datasource files are located under the datasources folder in Jigx Builder.

### Examples and code snippets

View common examples of using SQLite below, you can use these as a guideline to configure the same in your solutions.

#### sqlite in a jig file

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xDYOh1UAllO9EKKsEwuTi\_xjvmxdpuzf6r1ehwbzfseim8-5d0t6e1xgmxstbrrimg1083iphone13blueportrait.png" size="80" position="center" caption="Locally configured datasource" alt="Locally configured datasource"}
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

#### sqlite as a global datasource

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/yh7PKs\_rB9kz4BOnOu5EU\_k4oyl6hsldw50bdrzkk1aim8-5d0t6e1xgmxstbrrimg1083iphone13blueportrait.png" size="80" position="center" caption="Global configured datasource" alt="Global configured datasource"}&#x20;
{% endcolumn %}

{% column %}
Datasource with type `sqlite` as global datasource to select name, and email from the employee's table and to display the list of employees.

**Example:** \
See the full example on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-list/simple-lists/dynamic-data/employees-list.jigx)
{% endcolumn %}
{% endcolumns %}

:::CodeblockTabs&#x20;

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

### SQLite query cheatsheet

#### Count rows in the table

{% columns %}
{% column %}
In this example a SQLite query is used to count the rows in the **avatar** table.
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/HWIyEBofvpCdzrMXZJS3c\_sqlite-countrow.PNG" size="80" position="center" caption="Count rows" alt="Count rows"}&#x20;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="count-rows.sql" %}
```yaml
# count rows in a table
datasources:  
  row_count:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/avatar
  
      query: |
        SELECT COUNT(*) AS row_count
        FROM [default/avatar] 
```
{% endtab %}

{% tab title="count-rows-dd.jigx" %}
```yaml
title: Number of rows 
description: Use SQLite query to count the number of rows in the Avatar dynamic data table
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1489875347897-49f64b51c1f8?auto=format&fit=crop&q=60&w=800&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MXx8c3FsJTIwcXVlcnl8ZW58MHx8MHx8fDA%3D

# count rows in a table
datasources:  
  row_count:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/avatar
  
      query: |
        SELECT COUNT(*) AS row_count
        FROM [default/avatar] 
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Number of rows
            value: =@ctx.datasources.row_count.row_count
```
{% endtab %}
{% endtabs %}

#### Converting dates

Here is an example of using a SQLite query to convert dates in a dynamic data table.

![SQLite - Converting dates](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/XBSJF8_H6mFaRwMcXgr1v_sql-convertdates.png)

{% code title="converting-dates.sql" %}
```yaml
datasources:  
  actualDay:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/dates
  
      query: 
        SELECT 
        id, 
        STRFTIME('%d', json_extract(data, '$.date')) AS date,
        STRFTIME('%d.%m', json_extract(data, '$.finished_date')) AS finished_date,
        FROM [default/dates]
```
{% endcode %}

#### Joining data from tables and using subquery

Using a SQLite query, one can join data from different tables by utilizing subqueries. This allows for the combination of information from multiple tables based on specified conditions. By employing subqueries, one can retrieve and manipulate data ensuring accurate and comprehensive results. Below is an example of joining tables and then using a subquery.

&#x20;<img src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/6Rkwhr5x2QjySvZCCYyNZ_sql-join-subquery2.png" alt="Steps table" data-size="original">&#x20;

&#x20;<img src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/ymOmVsfObBApTdSuW94E4_sql-join-subquery1.png" alt="Strategy table" data-size="original">

{% code title="join-and-subquery.sql" %}
```yaml
datasources
  strategies-with-steps:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL

      entities:
        - entity: default/steps
        - entity: default/strategies

      query: |
        SELECT
          a.id AS id,
          json_extract(a.data, '$.name') AS name,
          json_extract(a.data, '$.strategy_id') AS strategy_id,
          json_extract(a.data, '$.isActive') AS isActive,
          json_extract(b.data, '$.step') AS step_title,
          json_extract(b.data, '$.step') AS step,
          (
          SELECT COUNT(*)
          FROM [default/steps] s
          WHERE json_extract(s.data, '$.strategy_id') = json_extract(a.data, '$.strategy_id')
          ) AS total_steps,
        FROM [default/strategies] a
        LEFT JOIN [default/steps] b ON json_extract(a.data, '$.strategy_id') = json_extract(b.data, '$.strategy_id')
```
{% endcode %}

#### Joining tables

Often you want to use data in your solution but the data is stored in different tables. Use a SQLite query to join the data from tables and extract the exact information you want to use. When joining two tables there must be the same identifier in both tables. In the example below both tables has a `$.date` column. _**Result**_: The result of the example below is  date: 5 finished\_date: 5.11

&#x20;![mood-notes table](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/dc6dS4tip_wOyz9MYbgm0_sql-jointable2.png)&#x20;

&#x20;![dates table](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/g7v7I8dD8own7zPsJF9dq_sql-jointables1.png) &#x20;

{% code title="join-table.sql" %}
```yaml
datasources:  
  mood-stats:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL

      entities:
        - entity: default/mood-notes
        - entity: default/dates

      query: |
        SELECT
          a.id AS id,
            STRFTIME('%d.%m', json_extract(a.data, '$.date')) AS date,
            json_extract(a.data, '$.day') AS numberOfDay,
            STRFTIME('%d', json_extract(a.data, '$.date')) AS day,
            json_extract(b.data, '$.mood') AS mood,
            json_extract(a.data, '$.date') AS dayDate
        FROM [default/dates] a
        LEFT JOIN [default/mood-notes] b ON STRFTIME('%d.%m', json_extract(a.data, '$.date')) = STRFTIME('%d.%m', json_extract(b.data, '$.date'))
        ORDER BY numberOfDay
```
{% endcode %}

#### JSON array length

The query below provides the JSON array length from a table called battles.

![Dynamic data table](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/5zo7bdA92zCAW5bMUESAl_sql-jsonarraylength.png)

{% code title="json-array-length.sql" %}
```yaml
--  array length if there is an array in the coloumn

datasources:
  battle-dynamic: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/battles
  
      query: |
        SELECT 
          id, 
          '$.name',
          '$.result_km',
          json_array_length(json_extract(data, '$.friends')) AS num_friends 
        FROM [default/battles] 
```
{% endcode %}
