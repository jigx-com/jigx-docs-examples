# form

Using forms in mobile apps enables users to effortlessly input and submit information, enhancing interaction and user engagement.

{% columns %}
{% column %}
The following components are available in a form:

1. [avatar-field](form/avatar-field.md)
2. [checkbox](form/checkbox.md)
3. [choice-field](form/choice-field.md)
4. [date-picker](form/date-picker.md)
5. [dropdown](form/dropdown.md)
6. [duration-picker](form/duration-picker.md)
7. [email-field](form/email-field.md)
8. [media-field](form/media-field.md)
9. [number-field](form/number-field.md)
10. [signature-field](form/signature-field.md)
11. [text-field](form/text-field.md)

These extra components allow for the easy input and collection of data. Using forms, records in a database can be created, updated, or deleted based on user input information.
{% endcolumn %}

{% column %}
Image\[]{alt="Form Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CmFxqLjk6bGCPvquRfLsB\_form.png" size="76" caption="Form Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/CmFxqLjk6bGCPvquRfLsB\_form.png" width="800" height="996" darkWidth="800" darkHeight="996"}
{% endcolumn %}
{% endcolumns %}

### Configuration options

Some properties are common to all components, see [Common component properties](form.md) for a list and their configuration options.

<table><thead><tr><th width="266.83984375">Core structure</th><th></th></tr></thead><tbody><tr><td><code>children</code></td><td><p>Define the content of the form. The following components can be used in the form:</p><ul><li><a href="form/choice-field.md">choice-field</a></li><li><a href="form/checkbox.md">checkbox</a></li><li><a href="form/date-picker.md">date-picker</a></li><li><a href="form/dropdown.md">dropdown</a></li><li><a href="form/duration-picker.md">duration-picker</a></li><li><a href="form/email-field.md">email-field</a></li><li><a href="entity/field-row.md">field-row</a></li><li><a href="form/media-field.md">media-field</a></li><li><a href="form/number-field.md">number-field</a></li><li><a href="entity/section.md">section</a></li><li><a href="form/signature-field.md">signature-field</a></li><li><a href="form/text-field.md">text-field</a></li></ul></td></tr><tr><td><code>instanceId</code></td><td>The unique identifier for the form.</td></tr></tbody></table>

<table><thead><tr><th width="270.57421875">Other options</th><th></th></tr></thead><tbody><tr><td><code>isDiscardChangesAlertEnabled</code></td><td>When set to <code>true</code> the modal window preventing accidental deletion of your data without saving will pop up.</td></tr><tr><td><code>initialValues</code></td><td>Specify the data to be used as <code>initialValues</code> for fields in the form. Using the <code>reset-state</code> action with <code>initialValues</code> does not clear the form, it resets the form back to it's <code>initialValue</code>. <em><strong>Tip</strong></em>: For <code>initialValues</code> on a to function <code>isDocument: true</code> in the datasource, this way you don't have to set it up in the individual components. It is set up in one place and the form will match the components to the column names of the datasource. See the example below for Form with initialValue.</td></tr></tbody></table>

<table><thead><tr><th width="264.63671875">State Configuration</th><th width="185.23046875">Key</th><th>Notes</th></tr></thead><tbody><tr><td><code>=@ctx.component.state.</code></td><td>data isValid isDirty response</td><td>State is the variable of the component.</td></tr><tr><td><code>=@ctx.solution.state.</code></td><td>activeItemId now</td><td>Global state variable that can be used throughout the solution.</td></tr></tbody></table>

### Examples and code snippets

#### Form for creating a record

{% columns %}
{% column %}
![Simple form](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/pB26E4FGL3st46LaEFHU8_ybxpqz2aem5zhq1e3bl8fformiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
Here is an example of a form for creating records in the database. See [submit-form](../Actions/submit-form.md) for information on how to create a record.

**Examples:**

See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/form/simple-form-submit.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="form (dynamic)" %}
```yaml
children:
  - type: component.form
    instanceId: simple-form
    options:
      children:
          - type: component.text-field
            instanceId: firstname
            options:
              label: First name
          - type: component.text-field
            instanceId: lastname
            options:
              label: Last name
          - type: component.email-field
            instanceId: email
            options:
              label: Email
          - type: component.number-field
            instanceId: phone
            options:
              label: Phone number
```
{% endcode %}

#### Form for updating records

{% columns %}
{% column %}
&#x20;![Update data form](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/P9wR9HiQwsUX8AI1jmlK7_img8326iphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
This example shows how a form is used to update an existing records in the database. Notice that a new variable called **initialValue:** has been added, we load the data that we have stored in the database and then change it. See the [execute-entity](../Actions/execute-entity.md) action for information on how to update a record.

**Examples**: See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/form/update-form-submit.jigx).

**Datasource**: See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/form/update-form-submit.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="update-form (dynamic)" %}
```yaml
actions:
  - children:
       - type: action.execute-entity
         options:
          title: Update Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/form
          method: update
          data:
            id: =@ctx.datasources.form-update.id 
            firstname: =@ctx.components.firstname.state.value
            lastname: =@ctx.components.lastname.state.value
            email: =@ctx.components.email.state.value
            phone: =@ctx.components.phone.state.value
          onSuccess: 
            type: action.go-back
                
children:
  - type: component.form
    instanceId: form-update
    options:
      children:
          - type: component.text-field
            instanceId: firstname
            options:
              label: First name
              initialValue: =@ctx.datasources.form-update.firstname
          - type: component.text-field
            instanceId: lastname
            options:
              label: Last name
              initialValue: =@ctx.datasources.form-update.lastname
          - type: component.email-field
            instanceId: email
            options:
              label: Email
              keyboardType: email-address
              initialValue: =@ctx.datasources.form-update.email
          - type: component.number-field
            instanceId: phone
            options:
              label: Phone number
              keyboardType: number-pad
              initialValue: =@ctx.datasources.form-update.phone
```
{% endtab %}

{% tab title="Python" %}
```yaml
datasources:
  form-update:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/form
      query: |
        SELECT
          id,
          '$.firstname',
          '$.lastname',
          '$.phone',
          '$.email',
          '$.category'
        FROM [default/form] WHERE '$.category' = "update-form"
```
{% endtab %}

{% tab title="Ruby" %}
```ruby
message = "hello world"
puts message
```
{% endtab %}
{% endtabs %}

#### Form with section and field-row

{% columns %}
{% column %}
![Form with formating](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/6UJEs4mNKl_fBwZiECCwZ_byk8bnoerar2j2b-9colgform-with-sectioniphone13blueportrait.png)
{% endcolumn %}

{% column %}
This example shows how you can format your form with sections and field-rows to create a visually appealing form.

**Examples:**

See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/form/form-with-section.jigx).
{% endcolumn %}
{% endcolumns %}

{% code title="form-section (dynamic)" %}
```yaml
children:
  - type: component.form
    instanceId: personal-information-form
    options:
      children:
          - type: component.section
            options:
              title: Personal information
              children:
                  - type: component.field-row
                    options:
                      children:
                          - type: component.text-field
                            instanceId: firstname
                            options:
                              label: First name
                          - type: component.text-field
                            instanceId: lastname
                            options:
                              label: Last name
                  - type: component.field-row
                    options:
                      children:
                        - type: component.email-field
                          instanceId: email
                          options:
                            label: Email
                        - type: component.number-field
                          instanceId: phone
                          options:
                            label: Phone number
          - type: component.section
            options:
              title: Address information
              children:
                - type: component.text-field
                  instanceId: address
                  options:
                    label: Address
                - type: component.field-row
                  options:
                    children:
                      - type: component.text-field
                        instanceId: city
                        options:
                          label: City
                      - type: component.number-field
                        instanceId: zip
                        options:
                          label: Zip code
```
{% endcode %}

#### Form with initialValue

{% columns %}
{% column %}
In this example, you tap on a contact in the contact-list and the new-contact form opens with the contact's details loaded. For `initialValues` on a [form](https://docs.jigx.com/examples/form) to function the `isDocument: true` in the datasource is set, this way you don't have to set it up in the individual components. It is set up in one place under `InitialValue` and the form will match the components to the column names of the datasource.
{% endcolumn %}

{% column %}
&#x20;![Form preloaded with data](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-Wpxk0IZiomKR6km8Si7o3-20241111-172919.png)
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="new-contact.jigx" %}
```yaml
title: Add new contact
type: jig.default
icon: book-address

inputs:
  id: 
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
          uri: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80
        
children:
  - type: component.form
    instanceId: new-contact
    options:
# With isDocument: true in the datasource set, 
# you don't have to set initialValue up in the individual components.
# It is set up in one place and the form will match the components to the column
# names of the datasource.   
      initialValues: =@ctx.datasources.contactData
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.section
          options:
            title: Personal information
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  label: First name
              - type: component.text-field
                instanceId: lastName
                options:
                  label: Last name
              - type: component.email-field
                instanceId: email
                options:
                  label: Email
                  icon: email
              - type: component.number-field
                instanceId: phone
                options:
                  label: Phone number
                  icon: phone
        - type: component.section
          options:
            title: Business information
            children:
              - type: component.text-field
                instanceId: jobTitle
                options:
                  label: Position
              - type: component.text-field
                instanceId: companyName
                options:
                  label: Company Name
            
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Create Record
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/contacts
          method: create
          data:
            firstName: =@ctx.components.firstName.state.value
            lastName: =@ctx.components.lastName.state.value
            email: =@ctx.components.email.state.value
            phone: =@ctx.components.phone.state.value
            jobTitle: =@ctx.components.jobTitle.state.value
            companyName: =@ctx.components.companyName.state.value
```
{% endtab %}

{% tab title="contactData (datasource)" %}
```yaml
datasources:
  contactData: 
    type: datasource.sqlite
    options:
# The isDocument property for the datasource is set to true.
# As a result, the datasource will return as a single record to be displayed,
# instead of an array of records.  
      isDocument: true
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/contacts
      query: |
        SELECT 
          id,
          '$.firstName',
          '$.lastName',
          '$.jobTitle',
          '$.companyName',
          '$.phone',
          '$.email' 
        FROM 
          [default/contacts]
         WHERE
          id = @contactId
      queryParameters:
        contactId: =@ctx.jig.inputs.id
```
{% endtab %}

{% tab title="contact-list.jigx" %}
```yaml
title: Contacts
type: jig.list
icon: contact

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1528747045269-390fe33c19f2?w=500&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8Mnx8Y29udGFjdCUyMGxpc3R8ZW58MHx8MHx8fDA%3D

data: =@ctx.datasources.contacts
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.firstName & ' ' & @ctx.current.item.lastName
    subtitle: =@ctx.current.item.companyName
    description: =@ctx.current.item.email
    leftElement: 
      element: avatar
      text: A
    onPress: 
      type: action.go-to
      options:
        linkTo: form-initialvalue
        parameters: 
          id: =@ctx.current.item.id
```
{% endtab %}
{% endtabs %}
