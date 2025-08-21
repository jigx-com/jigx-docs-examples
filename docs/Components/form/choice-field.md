# choice-field

The choice-field component allows you to select one or more options from a predefined list. This enhances user experience by providing a straightforward way to make selections, such as choosing a setting, selecting a category, or picking an item from a list. Implementing a choice-field component involves defining the available options and efficiently handling the user's selection.

**Benefit:** Using the choice-field component over the [checkbox](checkbox.md) component eliminates the need to use numerous checkboxes and complex expressions to achieve the same outcome.

{% hint style="info" %}
&#x20;The `choice-field` component can be used independently or within a `form` component, each offering distinct benefits. As a standalone, it provides flexibility for isolated usage without requiring a form structure. When wrapped in a form, it leverages the form’s instanceId, enabling better coordination and usability when managing multiple fields in a jig.&#x20;
{% endhint %}

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-bBqh\_WETCy6CgvD8nBr8c-20240826-164834.png" size="80" position="center" caption="Choice-field" alt="Choice-field" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-bBqh\_WETCy6CgvD8nBr8c-20240826-164834.png" width="800" height="498" darkWidth="800" darkHeight="498"}

## Configuration options

Some properties are common to all components, see [Common component properties](choice-field.md) for a list and their configuration options.

<table><thead><tr><th width="211.2109375">Core structure for choice-field</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The unique identifier for the choice-field component.</td></tr><tr><td><code>label</code></td><td>Provide a label/name for the choice-field.</td></tr><tr><td><code>data</code></td><td>Use an expression that evaluates to an array of options.</td></tr><tr><td><code>item</code></td><td>The <code>item</code> property uses the component of <code>choice-field-item</code> that includes: <code>title</code> and <code>value</code>.</td></tr></tbody></table>

<table><thead><tr><th width="211.01953125">Other options</th><th></th></tr></thead><tbody><tr><td><code>errorText</code></td><td>Add text, string, or expressions to show text under the choice-field indicating an error/invalid value in the field. Text is shown in <code>isNegative</code> (red) styling.</td></tr><tr><td><code>helperText</code></td><td>Add text, string, or expressions to guide users by showing text under the choice-field. Helper text is displayed only when there is no errorText.</td></tr><tr><td><code>initialValue</code></td><td>The <code>initialValue</code> is the value that will be displayed in the choice-field when the form is initially loaded. You can use this property to preset the choice-field with a default value so that you do not have to manually select it, for example, on a yes/no choice the initial value can be set to no.</td></tr><tr><td><code>isHidden</code></td><td>If <code>true</code> the choice-field will be hidden on the form. If set to <code>false</code> the field will be shown.</td></tr><tr><td><code>isIgnored</code></td><td>When <code>true</code>, the field will be ignored when submitting the form and the content will not be stored.</td></tr><tr><td><code>isMultiple</code></td><td>Set to <code>true</code> allows you to select multiple items inside the choice-field. Set to <code>false</code> only allows a single selection in the choice-field.</td></tr><tr><td><code>isOptionalLabelHidden</code></td><td>If the field is optional you can turn off the "(optional)" label by setting this field to <code>true</code>. This property works in combination with <code>isRequired: false</code>.</td></tr><tr><td><code>isRequired</code></td><td>Set to <code>true</code> when the field is required. Useful when you use it in form submission. Set to <code>false</code> the choice-field is optional and will have (optional) in the label.</td></tr><tr><td><code>itemsPerRow</code></td><td>Number of choice boxes to show in each row. Supports multiline text.</td></tr><tr><td><code>nextProperty</code></td><td>Name of the property you want to focus next in the form when you use return/next on a keyboard.</td></tr><tr><td><code>style</code></td><td><code>isDisabled</code> - disables the choice-field preventing the selection of any of the choice-fields.</td></tr><tr><td><code>value</code></td><td>The value that the choice-field will output as its state.</td></tr></tbody></table>

<table><thead><tr><th width="268.37890625">Other options for choice-field-item</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The unique identifier for the choice-field-item component.</td></tr><tr><td><code>title</code></td><td>Text displayed on the choice-field item. You can add text, expressions or Text with Format in the field. Text with format includes, currency, decimal, dateTime and more. In most instances an expression similar to <code>=@ctx.current.item.option</code> is used to reference the datasource.</td></tr><tr><td><code>value</code></td><td>The value of the item. It has to be unique for each item and is usually the ID of the record from the datasource.</td></tr></tbody></table>

<table><thead><tr><th width="242.16796875">Actions</th><th></th></tr></thead><tbody><tr><td><code>onChange</code></td><td>The action is triggered when the content in the <code>choice-field-item</code> is changed. Use IntelliSense (ctrl+space) to see the list of available actions.</td></tr></tbody></table>

<table><thead><tr><th width="238.9765625">State Configuration</th><th width="160.3359375">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>selected value</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

## Considerations

* The choice-field component can only be used in a form component on a default jig.
* The choice-field is an input control.
* Only text can be displayed in the `title` property.
* Using `itemPerRow` for long text is not recommended due to the limited space available in each item and the need for visual consistency among the choices. The property supports up to two lines of text per item.

## Examples and code snippets

### Choice-field with single selection

{% columns %}
{% column %}
&#x20;![Choice-field](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-F2DMxwJXBGFyG_d-CSAoo-20240827-102857.png)&#x20;


{% endcolumn %}

{% column %}
In this example, a `choice-field` component is configured with basic Yes/No options. If you a new customer and select _Yes_, then a `when` property is used with an expression to display additional form fields for the customer to complete. If you an existing customer, select _No_ and click the _Register & place_ \*order \*button to `goTo` the product-item jig to place an order.

**Examples:** See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-single.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% code title="choice-field-single.jigx" %}
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
# If yes go to online-store.
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
{% endcode %}

### Choice-field with multiple selection

{% columns %}
{% column width="50%" %}
In this example, two `choice-field` components are used. The first is a single Yes/No selection to answer a question. The second choice-field is configured with a `when` property to only display is the Yes selection was made. The `isMultiple` property set to true allows multiple options to be selected in the component. Selecting submit uses an `info-modal` to show the form was successfully submitted.

**Examples:** See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-multiple.jigx).
{% endcolumn %}

{% column width="50%" %}
&#x20;![Multiple choice selection](https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-gDRUtCVRkFn3meuYK0sLO-20240826-150347.PNG)&#x20;


{% endcolumn %}
{% endcolumns %}

{% code title="choice-field-multiple.jigx" %}
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
{% endcode %}

## Loading of multiple selected options

In this example, we want to load the patient's form that they completed in the example above, and show their selected details and allergies. Each patient can have multiple allergies, and the data would be saved as an object in the database. To deserialize the object the `jsonProperties` property is configured with the column containing the object of multiple allergies. In the `choice-field` component the `intialValue` is then configured to return the selected allergies for the specific patient. The `execute-entity` action is configured to update the patient data.

::Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-92ZKPcpsy9TZXXSufKGm--20250318-105534.png" size="70" position="center" caption="Load multiple choices" alt="Load multiple choices" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-92ZKPcpsy9TZXXSufKGm--20250318-105534.png" width="800" height="790" darkWidth="800" darkHeight="790"}

{% tabs %}
{% tab title="update-patient-details.jigx" %}
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
            # using an expression we can see if there are allergies for the 
            # patient, if allergies column contains data,
            # then the Yes choice-field is populated.         
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
                # Show the selected patient's allergies using initialValue.
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
# Set up the action to update the patient's details and allergies.          
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
{% endtab %}

{% tab title="patient-list.jigx" %}
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
{% endtab %}
{% endtabs %}

### Choice-field with three items per row

{% columns %}
{% column %}
Image\[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-24aUnSddX6OuZIUtlEQRX-20240827-101917.PNG" size="70" position="center" caption="Items per row" alt="Items per row" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-24aUnSddX6OuZIUtlEQRX-20240827-101917.PNG" width="1240" height="2500" darkWidth="1240" darkHeight="2500"}
{% endcolumn %}

{% column %}
Using the `itemsPerRow` property in the choice-field component defines how many choice option items must be shown on each row. Keep in mind this is on a mobile device, having more than 3 could make the options hard to read.

**Examples:** See the full example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/choice-field/choice-field-items-per-row.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="choice-field-items-per-row.jigx" %}
```yaml
title: Choice-field-items per ro
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
{% endcode %}

### Choice-field with an initial selection

{% columns %}
{% column %}
In this example of the choice-field component the form opens with an option already selected. This is configured using an expression in the `initialValue` property. You can change the property. Note that the `onRefresh` event used to reset the form, resets the `choice-field` back to it's orginial state with the `initialValue`selected.

**Examples:** See the full example in [GitHub](choice-field.md).
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-GapegBAIHUNysuq5uSO2n-20240826-145351.PNG" size="70" position="center" caption="Choice-field" alt="Choice-field" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-GapegBAIHUNysuq5uSO2n-20240826-145351.PNG" width="1240" height="2500" darkWidth="1240" darkHeight="2500"}
{% endcolumn %}
{% endcolumns %}

{% code title="choice-field-initialvalue.jigx" %}
```yaml
title: choice-field with initial value selected
type: jig.default
# Header section with medium-height image.
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
# Data configuration - fetch shipping options from Dynamic Data database
datasources:
  shipping: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC  
      entities:
        - default/shipping  
      query: |
        SELECT 
        id, 
        '$.method', 
        '$.cost'
        FROM [default/shipping]
# Main UI structure.
children:
  - type: component.form
    instanceId: delivery
    options:
      children:
       # Choice field for shipping method selection.
        - type: component.choice-field
          instanceId: shipping-method
          options:
            # Pre-selected the first shipping method from the database.
            initialValue: =@ctx.datasources.shipping[0].method
            label: Choose your shipping method 
            # Bind data from shipping datasource.
            data: =@ctx.datasources.shipping
            item:
              type: component.choice-field-item
              options:
                # Display format: "method cost" (e.g., "Express $15.99").
                title: =(@ctx.current.item.method & ' ' &  @ctx.current.item.cost)
                # The actual value stored when this option is selected.
                value: =@ctx.current.item.method
# Action buttons section.
actions:
  - children:
      # Navigation button to go back to previous screen.
      - type: action.go-back
        options:
          title: Checkout
```
{% endcode %}

### Choice-field with onChange

{% columns %}
{% column %}
&#x20;![Choice-field onChange](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-pBfq4DkE6NxBZKZSx-03t-20240826-145121.png)&#x20;


{% endcolumn %}

{% column %}
In this example, when the `choice-field-item` is selected and `onChange` event triggers a `open-url` action providing the information on the holiday packages.

**Examples:** See the full example in [GitHub](choice-field.md).
{% endcolumn %}
{% endcolumns %}

{% code title="choice-field-onchange/jigx" %}
```yaml
title: Choice-field with onChange
type: jig.default
# Header section with medium-height travel-themed image.
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1618245318763-a15156d6b23c?q=80&w=1740&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
# Static datasource containing vacation package information.
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
# Main UI structure.
children:
  - type: component.form
    instanceId: island-holiday
    options:
      children:
        # Choice field for vacation package selection.
        - type: component.choice-field
          instanceId: select-package
          options:
            # Action triggered when user selects an option.
            onChange: 
              type: action.open-url
              options:
                # Open the URL of the selected package in browser/new tab.
                url: =@ctx.components.select-package.state.selected.url
            label: Select an island package
            # Bind data from the packages datasource.
            data: =@ctx.datasources.packages
            # Configure how the choice options are displayed.
            item:
              type: component.choice-field-item
              options:
                # Display format: "Destination starting from Price" 
                # (e.g., "Seychelles starting from $ 1500")
                title: =(@ctx.current.item.name & ' ' & 'starting from' & ' ' & @ctx.current.item.Price)
                value: =@ctx.current.item.name
                
```
{% endcode %}
