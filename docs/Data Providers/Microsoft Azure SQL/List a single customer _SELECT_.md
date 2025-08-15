# List a single customer (SELECT)

{% hint style="warning" %}
Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](docId:jrbaNsm-OJn3nf4_dn_Hu) instead. See [REST endpoints from Azure SQL](https://docs.jigx.com/microsoft-azure-sql) for more information.&#x20;
{% endhint %}

{% columns %}
{% column %}
### Scenario

View the customer's details by pressing on the customer in the list, which opens the customer's details in a default jig.

### Resources

* Scripts for creating Azure SQL tables and stored procedures: [Database Scripts](<Database Scripts.md>).
* [Configuring the SQL Connection](https://docs.jigx.com/configuring-the-sql-connection).
* This sample depends on [List customers (SELECT)](<List customers _SELECT_.md>).

### Jigx Code

The Azure SQL Docs solution is on [GitHub](https://github.com/jigx-com/jigx-samples/tree/main/guides/azure-sql-docs)&#x20;
{% endcolumn %}

{% column %}
&#x20;<img src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/eb8nMUangvEbz5PSFP_Cm_thursday-23-mar-2023-151127.PNG" alt="List &#x26; view customer detail" data-size="original">
{% endcolumn %}
{% endcolumns %}

### How it works

This example selects a customer from the list and uses the CustomerId to return the customer's details to the default jig on the device, using the SQL data provider's function, where it is stored in the SQLite database. In the default jig the data is selected from the SQLite database using a SQL query in a data source which in turn is used by the jig to render the details in entity fields. The functions used to return a single record use **forRowsWithMatchingIds: true**. Only records in the SQLite table with a matching id will be updated. When forRowsWithMatchingIds is false or omitted, all records in the SQLite table will be deleted, and only the records returned by the stored procedure, or query statement will be inserted.

### Functions

{% hint style="info" %}
The Jigx function is listed twice, once for executing a stored procedure and once for executing a query.
{% endhint %}

#### A store procedure-based version of get-customer.jigx

{% code title="get-customer.jigx" fullWidth="false" %}
```yaml
# Jigx SQL function executing a stored procedure to select only a single customer. 
provider: DATA_PROVIDER_SQL
connection: customer.azure # Use manage.jigx.com to configure a SQL connection
method: execute #Use SQL stored procedsure to interact with the data in SQL
query: |
procedure: sp_GetCustomerById
parameters:
  # The stored procedure has a required parameter called CustomerId. Therefore the value of the Jigx function's CustomerId parameter will be passed as a parameter to the stored procedure.
  CustomerId:
    type: string
    location: input
# One of the columns returned by the stored procedure is called id. Only records in the SQLite table with a matching id will be updated. When forRowsWithMatchingIds is false or omitted, all records in the SQLite table will be deleted, and only the records returned by the store procedure will be inserted.
forRowsWithMatchingIds: true
```
{% endcode %}

#### A query-based version of get-customer.jigx

{% code title="get-customers.jigx" fullWidth="false" %}
```yaml
# Jigx SQL function executing a stored procedure to select only a single customer. 
provider: DATA_PROVIDER_SQL
connection: customer.azure # Use manage.jigx.com to configure a SQL connection
method: query #Use SQL statements to interact with the data in SQL
query: |
query: |
  SELECT
    id,
    first_name,
    last_name,
    email,
    phone_number,
    address_line1,
    address_line2,
    city,
    state,
    zip_code,
    country
  FROM
    customers
  WHERE
    id = @CustomerId
parameters:
  # The SQL query has a where clause that contains CustomerId. Therefore the value of the Jigx function's CustomerId parameter will be used as the value of the @CustomerId token in the where clause.
  CustomerId:
    type: string
    location: input
# One of the columns returned by the query statement is called id. Only records in the SQLite table with a matching id will be updated. When forRowsWithMatchingIds is false or omitted, all records in the SQLite table will be deleted, and only the records returned by the query statement will be inserted.
forRowsWithMatchingIds: true
```
{% endcode %}

### Jigs

#### Modifying the list customers jig

The listCustomers.jigx file must be modified to include an onPress action. When pressing on a list item in the customer list, Jigx will navigate to the viewCustomer.jigx. **customerId** is specified as a `parameter` that should be passed to the viewCustomer.jigx, where it is used in the WHERE clause of the SQLite query to load the selected customer.

Add the onPress code to the bottom of the listCustomers.jigx file:

{% code title=" listCustomers.jigx" fullWidth="false" %}
```yaml
# A sample list jig that uses a SQL function to return and display a list of customers from Azure SQL.
title: List Customers
description: Show a list of all customers in a SQL database.
type: jig.list
icon: contact

# Header section displaying an image at the top of the screen.
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1553413077-190dd305871c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1035&q=80

# onFocus is triggered whenever the jig is displayed. The sync-entities action calls the Jigx SQL function and populates the local SQLite tables on the device with the data returned from Azure SQL.
onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL
    entities:
      - entity: customers
        function: get-customers

# The mydata data source selects the data from the local SQLite database.
datasources:
  mydata: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
  
      entities:
        - entity: customers
  
      query: |
        SELECT
          id,
          '$.first_name',
          '$.last_name',
          '$.email',
          '$.phone_number',
          '$.address_line1',
          '$.address_line2',
          '$.city',
          '$.state',
          '$.zip_code',
          '$.country'
        FROM
          [customers]

# The list and its list items are configured below. This is a list jig; therefore, its properties, such as data and item, are top-level properties.
# The data property binds the list to a specific data source.
data: =@ctx.datasources.mydata
# The item property specifies the list item type and its attributes.
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.first_name & ' ' & @ctx.current.item.last_name
    subtitle: =@ctx.current.item.email
    description: |
      =@ctx.current.item.address_line1 & ' ' & 
        @ctx.current.item.city & ' ' & 
        @ctx.current.item.state  & ' ' & 
        @ctx.current.item.zip_code
    label:
      title: =@ctx.current.item.country
    leftElement: 
      element: avatar
      # The text property of the left element is specified using a JSONata expression that builds a two-letter string by concatenating the first letters of the customer's first and last names.
      text: =$substring(@ctx.current.item.first_name,0,1) & $substring(@ctx.current.item.last_name,0,1)
    divider: solid
    # A go-to action is triggered when pressing on a list item.
    onPress: 
      type: action.go-to
      options:
        # The name of the jig to navigate to when the item is pressed.
        linkTo: viewCustomer
        parameters:
          # The id column of the current item being pressed on is passed as a parameter called customerId to the viewCustomer jig.
          customerId: =@ctx.current.item.id
```
{% endcode %}

#### View customer jig

The WHERE clause in the query contains a token for a `parameter` called `customerId` that is defined in `queryParameters` and is passed to the viewCustomer jig as an input from the listCustomer jig.

The `isDocument` property for the mydata datasource is set to `true`. As a result, the data source will return as a single record to be displayed on a form instead of an array of records.

The data on the jig displays using an `entity` and `entity- fields` component. If the data source returns an array, an entity component will automatically show the first record.

The YAML for viewing the selected customer is:

{% code title="viewCustomer.jigx" fullWidth="false" %}
```yaml
# A sample jig that uses a SQL function to return and display a customer's details from Azure SQL.
# The title property uses a JSONata expression to concatenate the customer's first and last names as the title of the jig.
title: =@ctx.datasources.mydata.first_name & ' ' & @ctx.datasources.mydata.last_name  
description: View customer details from Azure SQL
type: jig.default

# Header section displaying an image at the top of the screen.
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1553413077-190dd305871c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1035&q=80

# onFocus is triggered whenever the jig is displayed. The sync-entities action calls the Jigx SQL function and populates the local SQLite tables on the device with the data returned from Azure SQL.          
onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL
    entities:
      - entity: customers
        function: get-customer
        parameters:
          CustomerId: =@ctx.jig.inputs.customerId

datasources:
# The mydata data source selects the data from the local SQLite database.
# The where clause in the query contains a token for a parameter called customerId that is defined in queryParameters and is passed to the viewCustomer jig as an input from the listCustomer jig.
# The isDocument property for the mydata datasource is set to true. As a result, the data source will return as a single record to be displayed on a form instead of an array of records.
  mydata: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customers
      query: |
        SELECT
          id,
          '$.first_name',
          '$.last_name',
          '$.email',
          '$.phone_number',
          '$.address_line1',
          '$.address_line2',
          '$.city',
          '$.state',
          '$.zip_code',
          '$.country'
        FROM
          [customers]
        WHERE
          id = @CustomerId          
      queryParameters:
        CustomerId: =@ctx.jig.inputs.customerId
      isDocument: true

children:
# The data on the jig is displayed using an entity control and entity fields. If the data source returns an array, an entity control will automatically show the first record.
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer ID
            # The value of each field points to the field in the mydata data source. 
            value: =@ctx.datasources.mydata.id
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: First Name
                  value: =@ctx.datasources.mydata.first_name
              - type: component.entity-field
                options:
                  label: Last Name
                  value: =@ctx.datasources.mydata.last_name
        - type: component.entity-field
          options:
            label: Email
            value: =@ctx.datasources.mydata.email
            contentType: email
        - type: component.entity-field
          options:
            label: Address Line 1
            value: =@ctx.datasources.mydata.address_line1
        - type: component.entity-field
          options:
            label: Address Line 2
            value: =@ctx.datasources.mydata.address_line2
        - type: component.field-row
          options:
            children:
              - type: component.entity-field
                options:
                  label: City
                  value: =@ctx.datasources.mydata.city
              - type: component.entity-field
                options:
                  label: State
                  value: =@ctx.datasources.mydata.state                        
        - type: component.entity-field
          options:
            label: Zip
            value: =@ctx.datasources.mydata.zip_code                                  
```
{% endcode %}

### index

Add the list of customers jig to the home screen.

{% code title="index.jigx" fullWidth="false" %}
```yaml
name: azure-sql-docs
title: Azure SQL Docs
category: analytics

tabs:
  home:
    jigId: listCustomers
    icon: home-apps-logo
```
{% endcode %}
