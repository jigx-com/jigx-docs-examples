---
title: choice-field
slug: TV_2-choice
createdAt: Wed Aug 21 2024 06:41:27 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 29 2025 05:34:02 GMT+0000 (Coordinated Universal Time)
---

The choice-field component allows you to select one or more options from a predefined list. This enhances user experience by providing a straightforward way to make selections, such as choosing a setting, selecting a category, or picking an item from a list. Implementing a choice-field component involves defining the available options and efficiently handling the user's selection.

**Benefit:** Using the choice-field component over the [checkbox](./checkbox.md) component eliminates the need to use numerous checkboxes and complex expressions to achieve the same outcome.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-bBqh_WETCy6CgvD8nBr8c-20240826-164834.png" size="80" position="center" caption="Choice-field" alt="Choice-field"}

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure for choice-field** |                                                     |
| ----------------------------------- | -------------------------------------------------------------------------------------------------- |
| `instanceId`                        | The unique identifier for the choice-field component.                                              |
| `label`                             | Provide a label/name for the choice-field.                                                         |
| `data`                              |  Use an expression that evaluates to an array of options.                                          |
| `item`                              | The `item` property uses the component of `choice-field-item` that includes: `title` and `value`.  |

| **Other options**       |                                                                                             |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `errorText`             | Add text, string, or expressions to show text under the choice-field indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling.                                                                                                                                          |
| `helperText`            | Add text, string, or expressions to guide users by showing text under the choice-field. Helper text is displayed only when there is no errorText.       |
| `initialValue`          | The `initialValue` is the value that will be displayed in the choice-field when the form is initially loaded. You can use this property to preset the choice-field with a default value so that you do not have to manually select it, for example, on a yes/no choice the initial value can be set to no. |
| `isHidden`              | If `true` the choice-field will be hidden on the form. If set to `false` the field will be shown.   |
| `isIgnored`             | When `true`, the field will be ignored when submitting the form and the content will not be stored.   |
| `isMultiple`            | Set to `true` allows you to select multiple items inside the choice-field. Set to `false` only allows a single selection in the choice-field.       |
| `isOptionalLabelHidden` | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.     |
| `isRequired`            | Set to `true` when the field is required. Useful when you use it in form submission. Set to `false` the choice-field is optional and will have (optional) in the label.    |
| `itemsPerRow`           | Number of choice boxes to show in each row. Supports multiline text.     |
| `nextProperty`          | Name of the property you want to focus next in the form when you use return/next on a keyboard.  |
| `style`                 | `isDisabled` - disables the choice-field preventing the selection of any of the choice-fields.  |
| `value`                 | The value that the choice-field will output as its state.   |

| **Other options for choice-field-item** |     |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `instanceId`                            | The unique identifier for the choice-field-item component.  |
| `title`                                 | Text displayed on the choice-field item. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more. In most instances an expression similar to `=@ctx.current.item.option` is used to reference the datasource. |
| `value`                                 | The value of the item. It has to be unique for each item and is usually the ID of the record from the datasource.   |

| **Actions** |    |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `onChange`  | The action is triggered when the content in the `choice-field-item` is changed. Use IntelliSense (ctrl+space) to see the list of available actions.  |

| **State Configuration**  | **Key**              | **Notes**                                                         |
| ------------------------ | -------------------- | ----------------------------------------------------------------- |
| `=@ctx.component.state.` | selected&#xA;value   | - State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | * Global state variable that can be used throughout the solution. |

## Considerations

- The choice-field component can only be used in a form component on a default jig.
- The choice-field is an input control.
- Only text can be displayed in the `title` property.
- Using `itemPerRow` for long text is not recommended due to the limited space available in each item and the need for visual consistency among the choices. The property supports up to two lines of text per item.

## Examples and code snippets

:::::ExpandableHeading
### Choice-field with single selection

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
![Choice-field](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-F2DMxwJXBGFyG_d-CSAoo-20240827-102857.png "Choice-field")
:::

:::VerticalSplitItem
In this example, a `choice-field` component is configured with basic Yes/No options.  If you a new customer and select *Yes*, then a `when` property is used with an expression to display additional form fields for the customer to complete.
If you an existing customer, select *No* and click the *Register & place* *order *button to `goTo` the product-item jig to place an order.

**Examples:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-single.jigx).


:::
::::

:::CodeblockTabs
choice-field-single.jigx

```yaml
title: Basic Choice 
description: New customer
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1472851294608-062f824d29cc?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8NHx8c2hvcG9ubGluZSUyMHN0b3JlfGVufDB8fDB8fHww
datasources:
 select-option:
    type: datasource.static
    options:
      data:
        - id: 1
          option: Yes
        - id: 2
          option: No         
          
children:
  - type: component.form
    instanceId: inputValues
    options:
    isDiscardChangesAlertEnabled: false
      children:
        - type: component.choice-field
          instanceId: new-customer
          options:
            label: Are you a new customer?
            data: =@ctx.datasources.select-option
            item:
              type: component.choice-field-item
              options:
                title: =@ctx.current.item.option
                value: =@ctx.current.item.option
  - type: component.form
    instanceId: register
    when: =@ctx.components.new-customer.state.value ='Yes' ? true:false
    options:
      children:
 # If yes is selected in the choice-field the form displays.       
        - type: component.text-field
          instanceId: firstName
          options:
            label: Fist name
            isRequired: true
        - type: component.text-field
          instanceId: lastName
          options:
            label: Last name
            isRequired: true
        - type: component.email-field
          instanceId: email
          options:
            label: Email address
            isRequired: true
        - type: component.number-field
          instanceId: phoneNumber
          options:
            label: Mobile number   
        - type: component.text-field
          instanceId: Address
          options:
            label: Address
            isMultiline: true
              
# if yes go to online-store
actions:
  - children:
      - type: action.action-list
        options:
# Hide the button until the No option is selected.
# Then show the button and go to the order jig.        
          isHidden: =@ctx.components.new-customer.state.value ='No' ? false:true
          title: Place order
          isSequential: true
          actions:
            - type: action.go-to
              options:
                linkTo: component-product-item
      - type: action.execute-entity 
        options:
          style:
# Disable the button until all fields in the form are filled in.           
            isDisabled: =$not(@ctx.components.register.state.isValid)
# Hide the button until the Yes option is selected.
# Then show the button, register the customer in Dymanica Data
# Go to the order jig.            
          isHidden: =@ctx.components.new-customer.state.value = 'Yes' ? false:true
          title: Register
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/customer
          method: create
          onSuccess: 
            type: action.go-to
            options:
              linkTo: component-product-item
          data:
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            Address: =@ctx.components.Address.state.value
```
:::
:::::

:::::ExpandableHeading
### Choice-field with multiple selection

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, two `choice-field `components are used. The first is a single Yes/No selection to answer a question. The second choice-field is configured with a `when` property to only display is the Yes selection was made. The `isMultiple` property set to true  allows multiple options to be selected in the component. Selecting submit uses an `info-modal` to show the form was successfully submitted.

**Examples:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-multiple.jigx).


:::

:::VerticalSplitItem
![Multiple choice selection](https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-gDRUtCVRkFn3meuYK0sLO-20240826-150347.PNG "Multiple choice selection")
:::
::::

:::CodeblockTabs
choice-field-multiple.jigx

```yaml
title: Patient Details
description: Patient information
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1532938911079-1b06ac7ceec7?q=80&w=1632&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# Resets the component when pulling down on the jig.
# The form resets with the configured initialValues.  
onRefresh: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.new-patient.state.data
    
datasources:
  allergies: 
    type: datasource.static
    options:
      data:
        - id: 1
          allergen: legumes   
        - id: 2
          allergen: nuts  
        - id: 3
          allergen: shellfish  
        - id: 4
          allergen: milk      
        - id: 5
          allergen: eggs  
        - id: 6
          allergen: wheat   
          
  select-option:
    type: datasource.static
    options:
      data:
        - id: 1
          option: Yes
        - id: 2
          option: No
            
children:
  - type: component.form
    instanceId: new-patient
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: firstName
          options:
            label: Fist name
            isRequired: true
        - type: component.text-field
          instanceId: lastName
          options:
            label: last name
            isRequired: true
        - type: component.email-field
          instanceId: email
          options:
            label: Email address
            isRequired: true
        - type: component.choice-field
          instanceId: select
          options:
            itemsPerRow: 2
            label: Do you have Allergies 
            data: =@ctx.datasources.select-option
            item:
              type: component.choice-field-item
              options: 
                title: =@ctx.current.item.option
                value: =@ctx.current.item.option
            
        - type: component.section
          when: =@ctx.components.select.state.value ='Yes' ? true:false
          options:
            title: What are you allergic to?
            children:
            - type: component.choice-field
              instanceId: allery
              options:
            # isMultiple allows for multiple selection
                isMultiple: true
                isRequired: true
                errorText: Required
            # Place the choice items two in a row     
                itemsPerRow: 2
                label: Patient Allergies
                data: =@ctx.datasources.allergies
                item:
                  type: component.choice-field-item
                  options:
                    title: =@ctx.current.item.allergen 
                    value: =@ctx.current.item.id
          
actions:
  - children:
      - type: action.execute-entity
        options:
          title: submit
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/patient
          method: create
          onSuccess: 
            type: action.info-modal
            options:
              modal:
                element: 
                  type: icon
                  icon: check
                  color: positive
                title: Form Submitted
                buttonText: Close
          data:
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            allergies: =@ctx.components.allery.state.selected
```
:::
:::::

::::ExpandableHeading
### Loading of multiple selected options

In this example, we want to load the patient's form that they completed in the example above, and show their selected details and allergies. Each patient can have multiple allergies, and the data would be saved as an object in the database. To deserialize the object the `jsonProperties` property is configured with the column containing the object of multiple allergies. In the `choice-field` component the `intialValue` is then configured to return the selected allergies for the specific patient. The `execute-entity` action is configured to update the patient data.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-92ZKPcpsy9TZXXSufKGm--20250318-105534.png" size="70" position="center" caption="Load multiple choices" alt="Load multiple choices"}

:::CodeblockTabs
update-patient-details.jigx

```yaml
title: Patient Details
description: Patient information
type: jig.default
# Add the input to receive the id for the specific patient 
inputs:
  patientId: 
    type: string
    required: true

header:
  type: component.jig-header
  options:
    height: medium
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1532938911079-1b06ac7ceec7?q=80&w=1632&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# Resets the component when pulling down on the jig.
# The form resets with the configured initialValues. 
onRefresh: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.new-patient.state.data
    
datasources:
  allergies: 
    type: datasource.static
    options:
      data:
        - id: 1
          allergen: legumes   
        - id: 2
          allergen: nuts  
        - id: 3
          allergen: shellfish  
        - id: 4
          allergen: milk      
        - id: 5
          allergen: eggs  
        - id: 6
          allergen: wheat   
          
  select-option:
    type: datasource.static
    options:
      data:
        - id: 1
          option: Yes
        - id: 2
          option: No
# The datasource used to return the patient details.
# queryParameter references the patientId input from the list
# jsonProperties is specified to deserialize the allergies object,
# allowing it to be loaded in the choice field as an initialValue       
  patient:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/patient
  
      query: 
        SELECT 
        id, 
        '$.firstName',
        '$.lastName',
        '$.email',
        '$.allergies'
        FROM [default/patient] 
        WHERE id = @patientId
      queryParameters:
        patientId: =@ctx.jig.inputs.patientId
      jsonProperties: 
        - allergies
      
children:
  - type: component.form
    instanceId: new-patient
    options:   
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: firstName
          options:
            initialValue: =@ctx.datasources.patient.firstName
            label: Fist name
            isRequired: true
        - type: component.text-field
          instanceId: lastName
          options:
            initialValue: =@ctx.datasources.patient.lastName
            label: last name
            isRequired: true
        - type: component.email-field
          instanceId: email
          options:
            initialValue: =@ctx.datasources.patient.email
            label: Email address
            isRequired: true
        - type: component.choice-field
          instanceId: select
          options:
# For this choice-field we do not save the value in the datasource, 
# Using an expression we can see if there are allergies for the patient,
# if allergies column contains data, then the Yes choice-field is populated.         
            initialValue: =$exists(@ctx.datasources.patient.allergies) ? 'Yes':'No'
            itemsPerRow: 2
            label: Do you have Allergies 
            data: =@ctx.datasources.select-option
            item:
              type: component.choice-field-item
              options: 
                title: =@ctx.current.item.option
                value: =@ctx.current.item.option
            
        - type: component.section
          options:
            title: What are you allergic to?
            children:
            - type: component.choice-field
              instanceId: allergy       
              options:
# Show the selected patient's allergies using initialValue
                initialValue: =@ctx.datasources.patient.allergies.id
                isMultiple: true
                isRequired: true
                errorText: Required
                itemsPerRow: 2
                label: Patient Allergies
                data: =@ctx.datasources.allergies
                item:
                  type: component.choice-field-item
                  options:
                    title: =@ctx.current.item.allergen 
                    value: =@ctx.current.item.id
# Set up the action to update the patient's details and allergies          
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Update
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/patient
          method: update
          onSuccess: 
            type: action.info-modal
            options:
              modal:
                element: 
                  type: icon
                  icon: check
                  color: positive
                title: Form Submitted
                buttonText: Close
          data:
            id: =@ctx.jig.inputs.patientId
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            allergies: =@ctx.components.allergy.state.selected
```

patient-list.jigx

```yaml
title: Update Patient list
type: jig.list
icon: doctor-consultation-chat-1

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1532938911079-1b06ac7ceec7?q=80&w=1632&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

onFocus:
  type: action.action-list
  options:
    isSequential: true
    actions:
      - type: action.sync-entities
        options:
          provider: DATA_PROVIDER_DYNAMIC
          entities:
            - default/patient
       
datasources:
  patient-list: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/patient
  
      query: 
        SELECT 
        id, 
        '$.firstName',
        '$.lastName',
        '$.email',
        '$.allergies'
        FROM [default/patient] 

data: =@ctx.datasources.patient-list
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstName
    subtitle: =@ctx.current.item.lastName
    rightElement: 
      element: button
      title: View
      onPress: 
        type: action.go-to
        options:
          linkTo: choice-field-multiple
          parameters:
            patientId: =@ctx.current.item.id
```
:::
::::

:::::ExpandableHeading
### Choice-field with 3 items per row

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-24aUnSddX6OuZIUtlEQRX-20240827-101917.PNG" size="70" position="center" caption="Items per row" alt="Items per row"}
:::

:::VerticalSplitItem
Using the `itemsPerRow` property in the choice-field component defines how many choice option items must be shown on each row. Keep in mind this is on a mobile device, having more than 3 could make the options hard to read.

**Examples:**
See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-items-per-row.jigx).


:::
::::

:::CodeblockTabs
choice-field-items-per-row\.jigx

```yaml
title: Choice-field-items per row
description: Customer Survey
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1628313388777-9b9a751dfc6a?q=80&w=1548&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

datasources:
  customer-satisfaction: 
    type: datasource.static
    options:
      data:
        - id: 1
          option: 😀 Happy
        - id: 2
          option: 😕 Neutral  
        - id: 3
          option: 😡 Sad 

children:
  - type: component.form
    instanceId: customer-survey
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.choice-field
          instanceId: satisfaction
          options:
            itemsPerRow: 3
            label: How satisfied were you with our service today?
            data: =@ctx.datasources.customer-satisfaction
            item:
              type: component.choice-field-item
              options:
                title: =@ctx.current.item.option
                value: =@ctx.current.item.option
actions:
  - children:
      - type: action.execute-entity
        options:
          title: submit
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/customer
          method: create
          onSuccess: 
            type: action.info-modal
            options:
              modal:
                element: 
                  type: image
                  uri: https://images.unsplash.com/photo-1643878037082-ba1fd9a60b16?q=80&w=1632&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
                title: Survey complete
                buttonText: Thank you
          data:
            satisfaction: =@ctx.components.satisfaction.state.value
```
:::


:::::

:::::ExpandableHeading
### Choice-field with an initial selection

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example of the choice-field component the form opens with an option already selected. This is configured using an expression in the  `initialValue` property. You can change the property. Note that the `onRefresh` event used to reset the form, resets the `choice-field` back to it's orginial state with the `initialValue`selected.

**Examples:**
See the full example in [GitHub]("https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-initialvalue.jigx).


:::

:::VerticalSplitItem
::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-GapegBAIHUNysuq5uSO2n-20240826-145351.PNG" size="70" position="center" caption="Choice-field" alt="Choice-field"}
:::
::::

:::CodeblockTabs
choice-field-initialvalue.jigx

```yaml
title: choice-field with initial value selected
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1617347454431-f49d7ff5c3b1?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MjN8fG9ubGluZSUyMGRlbGl2ZXJ5fGVufDB8fDB8fHwy
# Set the component back to the initialValue when refreshed.
onRefresh: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.shipping-method.state.value

datasources:
  shipping: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/shipping
  
      query: SELECT id, '$.method', '$.cost' FROM [default/shipping]

children:
  - type: component.form
    instanceId: delivery
    options:
      children:
        - type: component.choice-field
          instanceId: shipping-method
          options:
            initialValue: =@ctx.datasources.shipping[0].method
            label: Choose your shipping method 
            data: =@ctx.datasources.shipping
            item:
              type: component.choice-field-item
              options:
                title: =(@ctx.current.item.method & ' ' &  @ctx.current.item.cost)
                value: =@ctx.current.item.method
actions:
  - children:
      - type: action.go-back
        options:
          title: Checkout
```
:::
:::::

:::::ExpandableHeading
### Choice-field with onChange
::::VerticalSplit{layout="right"}
:::VerticalSplitItem
![Choice-field onChange](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-pBfq4DkE6NxBZKZSx-03t-20240826-145121.png "Choice-field onChange")
:::

:::VerticalSplitItem
In this example, when the `choice-field-item` is selected and `onChange` event triggers a `open-url` action providing the information on the holiday packages.

**Examples:**
See the full example in [GitHub]("https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-onchange.jigx).


:::
::::

:::CodeblockTabs
choice-field-onchange/jigx

```yaml
title: Choice-field with onChange
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1618245318763-a15156d6b23c?q=80&w=1740&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

datasources:
  packages:
    type: datasource.static
    options:
      data: 
        - name: Seychelles
          days: 30
          description: "10 days in luxury accomodation"
          Price: "$ 1500"
          url: https://www.clubmed.co.za/d/indian-ocean/seychelles
        - name: Maldives
          days: 60
          description: "7 days experience cultural activities"
          Price: "$ 1000"
          url: https://www.clubmed.co.za/d/indian-ocean/maldives
        - name: Mauritius
          days: 120
          description: "8 days includes watersports"   
          Price: "$ 2350"
          url: https://www.clubmed.co.za/d/indian-ocean/mauritius
        - name: Indonesia
          days: 95
          description: "15 days all inclusive experience"
          Price: "$ 3760"
          url: https://www.clubmed.co.za/d/asia/indonesia

children:
  - type: component.form
    instanceId: island-holiday
    options:
      children:
        - type: component.choice-field
          instanceId: select-package
          options:
            onChange: 
              type: action.open-url
              options:
                url: =@ctx.components.select-package.state.selected.url
            label: Select an island package
            data: =@ctx.datasources.packages
            item:
              type: component.choice-field-item
              options:
                title: =(@ctx.current.item.name & ' ' & 'starting from' & ' ' & @ctx.current.item.Price)
                value: =@ctx.current.item.name
                
```
:::
:::::

