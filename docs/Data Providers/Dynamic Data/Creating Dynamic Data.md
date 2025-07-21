---
title: Creating Dynamic Data
slug: 4lPS-creating-data-using-a-form
description: Learn how to create a form using the default Jig type and save employee data with this comprehensive document. Follow the step-by-step instructions to define form fields, configure the Jig, and add YAML code. Discover how to create an action for data savi
createdAt: Wed Jul 13 2022 10:20:52 GMT+0000 (Coordinated Universal Time)
updatedAt: Thu Mar 06 2025 08:30:25 GMT+0000 (Coordinated Universal Time)
---

Creating Dynamic Data can be achieved in several ways, one of which is by using a form. In this example, we will demonstrate how to create a new employee form that will create the employee table, columns, and data record in the Dynamic Data database when the form is submitted.

## Data provider, jig, component & action

1. **default.jigx** is the database where the Dynamic Data table is defined.
2. [jig.default](<./../../Jig Types/jig_default.md>) is the type of jig we will use to contain the form.
3. [form](./../../Components/form.md) is the component used with text and date fields.
4. [submit-form](./../../Actions/submit-form.md) is the action that executes the create method of the Dynamic Dataprovider

## Examples and code snippets

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-i6ehWvPp7BFJyRJURpPe2-20250306-083004.png" size="66" position="center" caption="Form creating Dynamic Data" alt="Form creating Dynamic Data"}

![Dynamic data database ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BBlDwFNCg9r4DSlmAFOO8_dd-employee-mngt.png "Dynamic data database ")

### Create the Dynamic Data table

:::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In Jigx Builder under the databases folder in the **default.jigx** file the employee table is added. This will create the table in Dynamic Data.
:::

::::VerticalSplitItem
:::CodeblockTabs
default.jigx

```yaml
tables:
  employee: null
```

:::
::::
:::::

### Create the jig, form and action

The code example below is for the `jig.default` with the `component.form` that uses `componet.text` and `component.date-picker` to create the fields on the form. The `action.submit-form` executes the `DATA_PROVIDER_DYNAMIC` that uses the `save/create` method to create columns and data records.

:::CodeblockTabs
new-employee-form.jigx

```yaml
title: New Employee
description: Employee form
# use the default jig as the container for the form
type: jig.default
icon: person-task-2

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1522202176988-66273c2fd55f?q=80&w=1471&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.section
    options:
      title: Personal Information
      children:
        # add the form component with fields to capture the dynamic data record
        - type: component.form
          # The id is used in the action for context to the fields which crete the columns and data
          instanceId: form-employee
          options:
            children:
              - type: component.text-field
                # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                instanceId: first_name
                options:
                  label: First Name
              - type: component.text-field
                # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                instanceId: last_name
                options:
                  label: Last Name
              - type: component.text-field
                # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                instanceId: address
                options:
                  label: Address
              - type: component.text-field
                # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                instanceId: contact
                options:
                  label: Contact Information
              - type: component.text-field
                # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                instanceId: email
                options:
                  label: Email
              - type: component.section
                options:
                  title: Employment Information
                  children:
                    - type: component.text-field
                      # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                      instanceId: job_title
                      options:
                        label: Job Title
                    - type: component.text-field
                      # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                      instanceId: department
                      options:
                        label: Department
                    - type: component.date-picker
                      # The name in the instanceId becomes the column name and the value entered in the field becomes the column data value
                      instanceId: start_date
                      options:
                        label: Start Date
actions:
  - children:
      # use the submit form action to execute the create/save method of the Dynamic Data provider.
      - type: action.submit-form
        options:
          # The formId is used to get the context to the fields and values that specify the columns and data
          formId: form-employee
          # specify the Dynamic Data provider to store the employees data record
          provider: DATA_PROVIDER_DYNAMIC
          title: Create Record
          entity: default/employee
          method: save # use the create or save method, the first exection will create columns and records, the second will create data records as the columns already exist.
          onSuccess:
            type: action.go-back
```

index.jigx

```yaml
name: employees
title: Employees
category: business

tabs:
  home:
    jigId: new-employee-form
    icon: home-apps-logo
```

:::

### View the Dynamic Data in Jigx Management

1. Open [Management](https://docs.jigx.com/management-overview) , navigate to your solution (employees).
2. Navigate to **Data** option
3. Click on the **employee table** and view the **data record** you just created.
