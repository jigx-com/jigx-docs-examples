---
title: Update a customer (UPDATE)
slug: bm53-updating-a-record
description: Learn how to use a default jig with a form to execute SQL commands and update customer records. This document highlights the importance of updating data in both the local SQLite database and the backend system for optimal user experience. It also includes
createdAt: Wed Mar 15 2023 12:45:29 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Nov 05 2024 11:40:00 GMT+0000 (Coordinated Universal Time)
---

:::hint{type="warning"}
Best practice for production apps is to use REST as the data layer to access data and not directly integrate to SQL using the SQL data provider. The SQL data provider will be squiggled in blue to indicate it is not recommended, together with a message to use [REST](docId\:jrbaNsm-OJn3nf4_dn_Hu) instead. See [REST endpoints from Azure SQL](docId\:eOUi2cPYynsdRuK-TobDp) for more information. &#x20;
:::

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
## **Scenario**

This example uses a default jig with a form that executes an SQL command to update a customer record.&#x20;

## **Resources**

- Scripts for creating Azure SQL tables and stored procedures: [Database Scripts](<./Database Scripts.md>).&#x20;
- [Configuring the SQL Connection]() &#x20;
- This sample depends on [List a single customer (SELECT)](<./List a single customer _SELECT_.md>).

## Jigx Code

The Azure SQL Docs solution is on <a href="https://github.com/jigx-com/jigx-samples/tree/main/guides/azure-sql-docs" target="_blank">GitHub.</a>
:::

:::VerticalSplitItem
![](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/F2u40_emrBYicR6Oo1HBd_saturday-25-mar-2023-113958.PNG "Update customer")
:::
::::

## How it works

- The `execute-entity` action allows you to specify the function parameters and their values, as well as the data properties for the SQLite table. You have more granular control over the values being saved and can include expressions. The example below uses an `execute- entity` action and maps both the parameters of the jig function and the SQLite data in the action's configuration.
- To improve the user experience, data displayed after it has been created or updated should be updated in the local SQLite database and the backend SQL system at the same action.&#x20;
- If the data is only submitted to the backend system, it must be synced back to the device before the local tables are updated, and the information can be displayed. This can cause a significant lag and latency in the user's experience. 
- The example below updates the data in Azure SQL and the SQLite database on the device when the user presses the Save button. This is the best practice for building responsive user experiences when working with remote data. See the [Data lifecycles in Jigx]() section of the documentation for a detailed explanation.

## Functions

### A store procedure-based version of update-customer.jigx

The **stored procedure** was designed to create a new record in Azure SQL if no matching id is found. If the id already exists, the Azure SQL record is updated. The same stored procedure is used for creating a new customer and updating a customer.

:::CodeblockTabs
update-customer.jigx

```yaml
# Jigx SQL function executing a stored procedure to create a new customer record. 
provider: DATA_PROVIDER_SQL
connection: customer.azure # Use manage.jigx.com to configure a SQL connection
method: execute #Use SQL stored procedure to interact with the data in SQL
procedure: sp_InsertOrUpdateCustomer
# The stored procedure parameters are automatically populated by Jigx with the matching function parameters.
parameters:
  CustomerId:
    type: string
    location: input
    required: true
  FirstName:
    type: string
    location: input
    required: true
  LastName:
    type: string
    location: input
    required: true
  Email:
    type: string
    location: input
    required: true
  PhoneNumber:
    type: string
    location: input
    required: true
  AddressLine1:
    type: string
    location: input
    required: true
  AddressLine2:
    type: string
    location: input
    required: false
  City:
    type: string
    location: input
    required: true
  ZipCode:
    type: string
    location: input
    required: true
  State:
    type: string
    location: input
    required: true
  Country:
    type: string
    location: input
    required: true

```
:::

### A query-based version of update-customer.jigx

The **SQL query** version of create-customer.jigx below only creates a new record. It does not contain update like like the stored procedure above. The only reason for this difference is to provide an alternative example and SQL logic.

:::CodeblockTabs
create-customer.jigx

```yaml
# Jigx SQL function executing a sql query to update a customer record in Azure SQL. 
provider: DATA_PROVIDER_SQL
connection: customer.azure # Use manage.jigx.com to configure a SQL connection
method: query #Use SQL statements to interact with the data in SQL
query: |
  UPDATE customers
    SET
      first_name = @FirstName,
      last_name = @LastName,
      email = @Email,
      phone_number = @PhoneNumber,
      address_line1 = @AddressLine1,
      address_line2 = @AddressLine2,
      city = @City,
      state = @State,
      zip_code = @ZipCode,
      country = @Country
    WHERE
      id = @CustomerId
# Jigx automatically replaces the tokens in the SQL query with the matching function parameters. 
parameters:
  CustomerId:
    type: string
    location: input
    required: true
  FirstName:
    type: string
    location: input
    required: true
  LastName:
    type: string
    location: input
    required: true
  Email:
    type: string
    location: input
    required: true
  PhoneNumber:
    type: string
    location: input
    required: true
  AddressLine1:
    type: string
    location: input
    required: true
  AddressLine2:
    type: string
    location: input
    required: false
  City:
    type: string
    location: input
    required: true
  ZipCode:
    type: string
    location: input
    required: true
  State:
    type: string
    location: input
    required: true
  Country:
    type: string
    location: input
    required: true

```
:::

## Jigs

### Modify the view customer jig

- The viewCustomers.jigx file must be modified to include a jig-level action, adding the **Edit a customer** button. When pressing the action button at the bottom of the viewCustomers jig, Jigx will navigate to the editCustomer jig.
- The** **customer's id** **is used as a parameter in the `GoTo` action. The `custId `parameter is passed to the viewCustomer jig.&#x20;

:::CodeblockTabs
listCustomers.jigx

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
        functionParameters:
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
            label: Phone Number
            value: =@ctx.datasources.mydata.phone_number
            contentType: phone
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
            
# Edit customer button to navigate to the newCustomer jig
actions:
  - children:
      - type: action.go-to
        options:
          title: Edit Customer
          linkTo: updateCustomer
          parameters:
            custId: =@ctx.datasources.mydata.id
```
:::

### The update customer jig

- Use an `execute-entity` action to submit the values of the components to the function to update Azure SQL and to save the new customer to the local SQLite database.
- When the `execute-entity` action type is used to save the values of the controls on a form, the form is unaware of the saved state, and **isDiscardChangesAlertEnabled** needs to be set to `false` to avoid seeing the dialog even when data has been saved.&#x20;
- Set the components on the form's value properties to the values from the `mydata` data source to display the existing values of the customer.

:::CodeblockTabs
newCustomer.jigx

```yaml
title: ='Update ' & @ctx.datasources.mydata.first_name & ' ' & @ctx.datasources.mydata.last_name  
description: Update a customer's information and save it to SQL Azure.
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

# Ensure we have the latest information for the customer by syncing the customer's data from Azure SQL
# onFocus is triggered whenever the jig is displayed. The sync-entities action calls the Jigx SQL function and populates the local SQLite tables on the device with the data returned from Azure SQL.          
onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL
    entities:
      - entity: customers
        function: get-customer
        functionParameters:
          CustomerId: =@ctx.jig.inputs.custId

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
        CustomerId: =@ctx.jig.inputs.custId
      isDocument: true

# A form control with input controls are used to capture the changes to the customer's information.
#The values from mydata is set to the value property of each control when the form loads.
children:
  - type: component.form
    instanceId: frmNewCustomer
    options:
      # When a form submit action is used to save the values of the controls on a form, the form will warn the user when navigating away without saving the form's content. 
      # When any other action type is used to save the values of the controls on a form, the form is unaware of the saved state, and isDiscardChangesAlertEnabled needs to be set to false to avoid seeing the dialog even when data has been saved. 
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: FirstName
                options:
                  label: First Name
                  #set the value property of the control to the value returned from the mydata datasource.
                  value: =@ctx.datasources.mydata.first_name
              - type: component.text-field
                instanceId: LastName
                options:
                  label: Last Name
                  value: =@ctx.datasources.mydata.last_name
        - type: component.email-field
          instanceId: Email
          options:
            label: Email
            value: =@ctx.datasources.mydata.email
            # The type of keyboard that will be displayed on iOS or Android.
            keyboardType: email-address
        - type: component.text-field
          instanceId: PhoneNumber
          options:
            label: Phone Number
            value: =@ctx.datasources.mydata.phone_number
            keyboardType: phone-pad
            # Set the type of text for this field. This will enforce a regex for this field of the type it is set to.
            textContentType: telephoneNumber
        - type: component.text-field
          instanceId: AddressLine1
          options:
            label: Address Line 1
            value: =@ctx.datasources.mydata.address_line1
            textContentType: streetAddressLine1
        - type: component.text-field
          instanceId: AddressLine2
          options:
            label: Address Line 2           
            textContentType: streetAddressLine2
            value: =@ctx.datasources.mydata.address_line2
            isRequired: false
        - type: component.text-field
          instanceId: City
          options:
            label: City
            value: =@ctx.datasources.mydata.city
            textContentType: addressCity
        # A dropdown control is used to list the USA states. 
        - type: component.dropdown
          instanceId: State
          options:
            label: State
            # The data source for the dropdown options is a static datasource defined in usa-states.jigx.
            data: =@ctx.datasources.usa-states
            value: =@ctx.datasources.mydata.state
            item:
              type: component.dropdown-item
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.code            
        - type: component.text-field
          instanceId: ZipCode
          options:
            label: Zip Code
            value: =@ctx.datasources.mydata.zip_code
            textContentType: postalCode
        - type: component.text-field
          instanceId: Country
          options:
            label: Country
            textContentType: countryName
            value: =@ctx.datasources.mydata.country
            style:
              # The dropdown only contains USA states.
              # Set the control to read only so the value cannot be changed to an unsupported country.
              isDisabled: true
actions:
  - children:
      # Use an execute entity action to submit the values of the controls to the Jigx function to update Azure SQL and to save the new customer to the local SQLite database.
      - type: action.execute-entity
        options:
          # The title of the save button.
          title: Update Customer
          # The data provider to use for the remote data. This solution uses Azure SQL.
          provider: DATA_PROVIDER_SQL
          # The name of the local SQLite database that the new record will be created in.
          entity: customers
          # The name of the Jigx function used to save the data to Azure SQL.
          function: create-customer
          # Set the function parameters to values of the controls on the form.
          functionParameters:
            CustomerId: =@ctx.jig.inputs.custId
            FirstName: =@ctx.components.FirstName.state.value
            LastName: =@ctx.components.LastName.state.value
            Email: =@ctx.components.Email.state.value
            PhoneNumber: =@ctx.components.PhoneNumber.state.value
            AddressLine1: =@ctx.components.AddressLine1.state.value
            AddressLine2: =@ctx.components.AddressLine2.state.value
            City: =@ctx.components.City.state.value
            ZipCode: =@ctx.components.ZipCode.state.value
            State: =@ctx.components.State.state.selected.code
            Country: =@ctx.components.Country.state.value
          # The command type to be executed on the local SQLite database.
          method: update
          # Navigate to the previous screen after the action has been performed.
          onSuccess: 
            type: action.go-back 
          # Set the column values of the new record that will be created in the local SQLite Customers table.
          data:
            id: =@ctx.jig.inputs.custId
            FirstName: =@ctx.components.FirstName.state.value
            LastName: =@ctx.components.LastName.state.value
            Email: =@ctx.components.Email.state.value
            PhoneNumber: =@ctx.components.PhoneNumber.state.value
            AddressLine1: =@ctx.components.AddressLine1.state.value
            AddressLine2: =@ctx.components.AddressLine2.state.value
            City: =@ctx.components.City.state.value
            ZipCode: =@ctx.components.ZipCode.state.value
            State: =@ctx.components.State.state.selected.code
            Country: =@ctx.components.Country.state.value   
          # Display a dialog box with a message if the new record is created successfully.    
          onSuccess: 
            description: Customer Updated Successfully
            title: Updated Created
          
```
:::

