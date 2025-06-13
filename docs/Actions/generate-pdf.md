# generate-pdf

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The generate-pdf action allows you to quickly create a PDF file version of HTML content, whether a receipt, report, form, or other document.

The URI of the generated file is returned and is available as part of the action instance output. When you tap the button, the app compiles the necessary information and generates a file you can save, or share instantly.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-kjDY250z7O_Flk4q6qp9u-20250218-113955.gif" size="60" position="center" caption="Generate a PDF file" alt="Generate a PDF file" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-kjDY250z7O_Flk4q6qp9u-20250218-113955.gif"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `html`             | Use standard HTML elements to ensure optimal formatting and compatibility when rendering content in the PDF file, for example, \<html>\<body>Invoices are provided monthly.\</body\</html>.&#xA;The HTML can be built up using JSONata or JavaScript.                    |
| `fileName`         | Give the PDF a name, this name is used as the local file name, and is referenced as part of the uri, which can be accessed via the action's instance output (`=@ctx.actions.generatePDF.outputs.uri`). &#xA;The .pdf extension is automatically added to the `fileName`. |
| `title`            | Provide the action button with a title, for example, Invoice.                                                                                                                                                                                                            |

| **Other options** |                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Select an [icon](#) to display when the action is configured as the secondary button or in a [header action](./../Components/jig-header.md).                                                                                                                                                                                                                                                                                       |
| `isHidden`        | `true` hides the action button, `false` shows the action button. Default setting is `false`.                                                                                                                                                                                                                                                                                                                                       |
| `styles`          | `isDanger` - Styles the action button in red or your brand's designated danger color.&#xA;`isDisabled` - Displays the action button as greyed out.&#xA;`isPrimary` - Styles the action button in blue or your brand's designated primary color.&#xA;`isSecondary` - Sets the action as a secondary button, accessible via the ellipsis. The `icon` property can be used when the action button is displayed as a secondary button. |

## Considerations

- You can reference the local PDF file using the action's output uri in other actions or components, `=@ctx.actions.generatePDF.outputs.uri`. For example, generate the PDF file then [share](./share.md) the file. The outputs is only supported within the context of that action. To use the outputs in components, either use the saved value or persist it to state.
- Depending on where you save and use the saved PDF, you might need to use [conversions](#).
- The .pdf extension is automatically added to the `fileName`.

## Examples and code snippets

### Basic generate a PDF and share

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-kjDY250z7O_Flk4q6qp9u-20250218-113955.gif" size="70" position="center" caption="Generate and share PDF" alt="Generate and share PDF" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-kjDY250z7O_Flk4q6qp9u-20250218-113955.gif"}
:::

:::VerticalSplitItem
In this example, an action list contains two actions: the first generates a PDF of a checklist, the second shares the PDF via a messaging app on the device.
:::
::::

:::CodeblockTabs
action-generate-pdf.jigx

```yaml
title: Site Checklist
type: jig.document
  
source:
  documentType: HTML
  # Use a datasource with the required raw HTML
  content: =@ctx.datasources.html-data.checklist-html
# Create an action list that will first create the PDF from the HTML,
# secondly share the pdf file via one of the devices messaging apps.          
actions:
  - children:
      - type: action.action-list
        options:
          title: Send checklist
          isSequential: true
          actions:
            # First action to create the pdf.
            - type: action.generate-pdf
              # Add an instanceId to use in the actions output expression.
              instanceId: share-pdf
              options: 
                # Provide the HTML of the checklist.  
                html: =@ctx.datasources.html-data.checklist-html
                # Provide the name of the pdf
                fileName: foreman-checklist
            # Add the second action to share out the pdf,
            # on one of the devices messaging apps.    
            - type: action.share
              options: 
                message: Completed morning checks on Site B
                subject: Site checks complete
                # Use the action instance output to reference the file.
                fileUri: =@ctx.actions.share-pdf.outputs.uri             
```

datasource (HTML)

```yaml
# Use a datasource with the required HTML
datasources:
    html-data:
      type: datasource.static
      options:
        data:
          - id: 1
            checklist-html: |
              <!DOCTYPE html>
                <html lang="en">
                <head>
                    <meta charset="UTF-8">
                    <meta name="viewport" content="width=device-width, initial-scale=1.0">
                    <title>Construction Site Checklist</title>
                    <style>
                        body {
                            font-family: Arial, sans-serif;
                            margin: 20px;
                            padding: 20px;
                            background-color: #f4f4f4;
                        }
                        .checklist {
                            background: #fff;
                            padding: 20px;
                            border-radius: 5px;
                            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
                        }
                        h2 {
                            text-align: center;
                        }
                        ul {
                            list-style: none;
                            padding: 0;
                        }
                        li {
                            margin: 10px 0;
                        }
                        input[type="checkbox"] {
                            margin-right: 10px;
                        }
                    </style>
                </head>
                <body>
                    <div class="checklist">
                        <h2>Construction Site Checklist</h2>
                        <ul>
                            <li><input type="checkbox"> Safety gear checked (helmets, vests, gloves, etc.)</li>
                            <li><input type="checkbox"> Equipment inspected and functional</li>
                            <li><input type="checkbox"> Site hazards identified and secured</li>
                            <li><input type="checkbox"> Workers briefed on tasks and safety</li>
                            <li><input type="checkbox"> Materials delivered and accounted for</li>
                            <li><input type="checkbox"> Work permits and documentation verified</li>
                            <li><input type="checkbox"> Emergency procedures reviewed</li>
                            <li><input type="checkbox"> Waste disposal managed</li>
                            <li><input type="checkbox"> Final site walk-through completed</li>
                        </ul>
                    </div>
                </body>
                </html>
```
:::

### Generate a pdf,  save and share&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, an action list contains three actions: the first generates a PDF for an invoice, the second saves it to the database, and the third shares the PDF via a messaging app on the device.  When saving the file to the database the file is converted from local-uri to data-uri for storage.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-mr09He1lx2C9ojC6KgBaZ-20250228-134244.gif" size="70" position="center" caption="Generate PDF, save & share" alt="Generate PDF, save & share" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-mr09He1lx2C9ojC6KgBaZ-20250228-134244.gif"}
:::
::::

:::CodeblockTabs
action-generate-pdf-save-share.jigx

```yaml
title: Monthly invoicing
description: Provide you details
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1450101499163-c8848c66ca85?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGludm9pY2luZ3xlbnwwfHwwfHx8MA%3D%3D    
  
children:
  - type: component.section
    options:
      title: Details
      children: 
        - type: component.form
          instanceId: inputValues
          options:
            children:
              - type: component.text-field
                instanceId: firstName
                options:
                  initialValue: John Smith
                  label: First name
                  isRequired: false
              - type: component.email-field
                instanceId: email
                options:
                  initialValue: john.smith@global.com
                  label: Email address
              - type: component.number-field
                instanceId: phoneNumber
                options:
                  initialValue: 23445634556
                  label: Mobile number
# Create an action list that will first create the PDF from the HTML,
# secondly save the PDF file to the dynamic database,
# thirdly share the pdf file via one of the devices messaging apps.                  
actions:
  - children:
      - type: action.action-list
        options:
          title: Send Invoice
          isSequential: true
          actions:
           # First action to generate the pdf.
            - type: action.generate-pdf
              instanceId: generate-pdf-id
              options:
                # Provide the HTML for the PDF file.
                html: |
                  <!DOCTYPE html>
                    <html lang="en">
                    <head>
                      <meta charset="UTF-8">
                      <meta name="viewport" content="width=device-width, initial-scale=1.0">
                      <title>Invoice</title>
                      <style>
                        body {
                          font-family: 'Arial', sans-serif;
                          margin: 0;
                          padding: 20px;
                          background-color: #f6f6f6;
                        }
                        .invoice-box {
                          max-width: 800px;
                          margin: auto;
                          padding: 30px;
                          border: 1px solid #eee;
                          box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
                          background-color: #fff;
                          color: #555;
                        }
                        .invoice-box table {
                          width: 100%;
                          line-height: 1.6;
                          text-align: left;
                          border-collapse: collapse;
                        }
                        .invoice-box table td {
                          padding: 5px;
                          vertical-align: top;
                        }
                        .invoice-box table tr td:nth-child(2) {
                          text-align: right;
                        }
                        .invoice-box table tr.top table td {
                          padding-bottom: 20px;
                        }
                        .invoice-box table tr.information table td {
                          padding-bottom: 40px;
                        }
                        .invoice-box table tr.heading td {
                          background: #eee;
                          border-bottom: 1px solid #ddd;
                          font-weight: bold;
                        }
                        .invoice-box table tr.details td {
                          padding-bottom: 20px;
                        }
                        .invoice-box table tr.item td {
                          border-bottom: 1px solid #eee;
                        }
                        .invoice-box table tr.item.last td {
                          border-bottom: none;
                        }
                        .invoice-box table tr.total td:nth-child(2) {
                          border-top: 2px solid #eee;
                          font-weight: bold;
                        }
                        h2, h3 {
                          margin: 0;
                        }
                      </style>
                    </head>
                    <body>
                      <div class="invoice-box">
                        <table cellpadding="0" cellspacing="0">
                          <!-- Invoice Header -->
                          <tr class="top">
                            <td colspan="2">
                              <table>
                                <tr>
                                  <td class="title">
                                    <h2>Company Name</h2>
                                  </td>
                                  <td>
                                    Invoice #: 12345<br>
                                    Created: January 1, 2025<br>
                                    Due: January 31, 2025
                                  </td>
                                </tr>
                              </table>
                            </td>
                          </tr>
                          <!-- Company & Customer Information -->
                          <tr class="information">
                            <td colspan="2">
                              <table>
                                <tr>
                                  <td>
                                    Company Name, Inc.<br>
                                    12345 Street Address<br>
                                    City, State, Zip
                                  </td>
                                  <td>
                                    Customer Name<br>
                                    Customer Company<br>
                                    67890 Customer Address
                                  </td>
                                </tr>
                              </table>
                            </td>
                          </tr>
                          <!-- Payment Method Details -->
                          <tr class="heading">
                            <td>Payment Method</td>
                            <td>Check #</td>
                          </tr>
                          <tr class="details">
                            <td>Check</td>
                            <td>1001</td>
                          </tr>
                          <!-- Itemized List of Services/Products -->
                          <tr class="heading">
                            <td>Item</td>
                            <td>Price</td>
                          </tr>
                          <tr class="item">
                            <td>Website Design</td>
                            <td>$300.00</td>
                          </tr>
                          <tr class="item">
                            <td>Hosting (3 months)</td>
                            <td>$75.00</td>
                          </tr>
                          <tr class="item last">
                            <td>Domain Registration (1 year)</td>
                            <td>$10.00</td>
                          </tr>
                          <!-- Total -->
                          <tr class="total">
                            <td></td>
                            <td>Total: $385.00</td>
                          </tr>
                        </table>
                      </div>
                    </body>
                    </html>
                # Give the pdf a name that is used when saved or shared.  
                fileName: invoice-1
           # Second action to save the file to the Dynamic database.   
            - type: action.execute-entity
              options: 
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/documents
                method: create
                data:
                  # Enter the file name for database storage.
                  fileName: invoice-1
                  date: =$now()
                  # Use the action instance output to reference the file.
                  file: =@ctx.actions.generate-pdf-id.outputs.uri
                # Convert the file from local-URI to data-URI for database storage.  
                conversions:
                  - property: file
                    from: local-uri
                    to: data-uri
            # Third action to share the file via the device's messaging app.        
            - type: action.share
              options:
                # Use the action instance output to reference the file.
                fileUri: =@ctx.actions.generate-pdf-id.outputs.uri
                # Provide a message and subject to accompany the share.
                message: Global Invoice 
                subject: Invoice for January
```
:::

### Generate pdf from JavaScript HTML function

This example demonstrates how to use a JavaScript function to generate an HTML invoice. The invoice is populated with customer details retrieved from a Dynamic Data datasource named invoices. The JavaScript function is referenced in an expression used by `action.generate-pdf`, after which the invoice is shared using the `action.share` via the device's apps.

![PDF from JavaScript function](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-wZMGFJvxtv3534txsjD9R-20250228-132836.png "PDF from JavaScript function")

:::CodeblockTabs
action-pdf-javascript.jigx

```yaml
title: Monthly invoicing
description: Provide your details
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1450101499163-c8848c66ca85?w=900&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTR8fGludm9pY2luZ3xlbnwwfHwwfHx8MA%3D%3D    
      
children:
  - type: component.section
    options:
      title: Details
      children: 
        - type: component.form
          instanceId: inputValues
          options:
            children:
              - type: component.text-field
                instanceId: customerCompany
                options:
                  initialValue: =@ctx.datasources.customer.customerCompany
                  label: First name
                  isRequired: false
              - type: component.text-field
                instanceId: firstName
                options:
                  initialValue: =@ctx.datasources.customer.firstName
                  label: First name
                  isRequired: false
              - type: component.email-field
                instanceId: email
                options:
                  initialValue: =@ctx.datasources.customer.email
                  label: Email address
              - type: component.number-field
                instanceId: phoneNumber
                options:
                  initialValue: =@ctx.datasources.customer.phoneNumber
                  label: Mobile number
# Create an action list that creates the PDF from the JavaScript HTML function,
# secondly share the pdf file via one of the devices apps.                      
actions:
  - children:
      - type: action.action-list
        options:
          title: Send Invoice
          isSequential: true
          actions:
            # First action to create the pdf.
            - type: action.generate-pdf
              instanceId: generate-pdf-id
              options:
                # Reference the JavaScript HTML function in an expression,
                # and provide the reference to the datasource for the inputs.
                html: 
                   =$html.generateHTML(@ctx.datasources.customer) 
                # Provide the name of the pdf.   
                fileName: invoice
            # Save the PDF to the database.    
            - type: action.execute-entity
              options: 
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/documents
                method: create
                data: 
                  fileName: invoice
                  date: =$now()
                  # Use the action instance output to reference the file.
                  file: =@ctx.actions.generate-pdf-id.outputs.uri
            # Add the second action to share out the pdf,
            # on one of the devices apps.       
            - type: action.share
              options:
                # Use the action instance output to reference the file.
                fileUri: =@ctx.actions.generate-pdf-id.outputs.uri
                message: Global Invoice 
                subject: Invoice for January 
```

datasource

```yaml
datasources:
  
  customer:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      # Use isDocument true to record a single record.
      isDocument: true
      entities:
        - default/invoices
  
      query: |
       SELECT id,
        '$.firstName',
        '$.email', 
        '$.phoneNumber',
        '$.customerCompany',
        '$.address'
       FROM [default/invoices] 
       WHERE firstName = 'John Smith'
```

html.js

```javascript
// Create a JS function that generates HTML, reference the input fields from the datasource
  export function generateHTML(invoiceInfo) {
     const { firstName, customerCompany, address } = invoiceInfo;
    // Specify what must be returned.
    return `
      <!DOCTYPE html>
      <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Invoice</title>
        <style>
              body {
                font-family: 'Arial', sans-serif;
                margin: 0;
                padding: 20px;
                background-color: #f6f6f6;
              }
              .invoice-box {
                max-width: 800px;
                margin: auto;
                padding: 30px;
                border: 1px solid #eee;
                box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
                background-color: #fff;
                color: #555;
              }
              .invoice-box table {
                width: 100%;
                line-height: 1.6;
                text-align: left;
                border-collapse: collapse;
              }
              .invoice-box table td {
                padding: 5px;
                vertical-align: top;
              }
              .invoice-box table tr td:nth-child(2) {
                text-align: right;
              }
              .invoice-box table tr.top table td {
                padding-bottom: 20px;
              }
              .invoice-box table tr.information table td {
                padding-bottom: 40px;
              }
              .invoice-box table tr.heading td {
                background: #eee;
                border-bottom: 1px solid #ddd;
                font-weight: bold;
              }
              .invoice-box table tr.details td {
                padding-bottom: 20px;
              }
              .invoice-box table tr.item td {
                border-bottom: 1px solid #eee;
              }
              .invoice-box table tr.item.last td {
                border-bottom: none;
              }
              .invoice-box table tr.total td:nth-child(2) {
                border-top: 2px solid #eee;
                font-weight: bold;
              }
              h2, h3 {
                margin: 0;
              }
            </style>
      </head>
      <body>
        <div class="invoice-box">
          <table cellpadding="0" cellspacing="0">
            <!-- Invoice Header -->
            <tr class="top">
              <td colspan="2">
                <table>
                  <tr>
                    <td class="title">
                      <h2>Global Inc</h2>
                    </td>
                    <td>
                      Invoice #: 12345<br>
                      Created: January 1, 2025<br>
                      Due: January 31, 2025
                    </td>
                  </tr>
                </table>
              </td>
            </tr>
            <!-- Company & Customer Information -->
            <tr class="information">
              <td colspan="2">
                <table>
                  <tr>
                  <!-- Specify the inputs from the datasource -->
                    <td>
                      ${firstName || ''}<br>
                      ${customerCompany || ''}<br>
                      ${address || ''}<br>
                    </td>
                    <td>
                      Global Inc<br>
                      67890 First Avenue,<br>
                      New York,<br>
                      34567
                    </td>
                  </tr>
                </table>
              </td>
            </tr>
            <!-- Remaining HTML content -->
            <!-- Payment Method Details -->
                <tr class="heading">
                  <td>Payment Method</td>
                  <td>Check #</td>
                </tr>
                <tr class="details">
                  <td>Check</td>
                  <td>1001</td>
                </tr>
                <!-- Itemized List of Services/Products -->
                <tr class="heading">
                  <td>Item</td>
                  <td>Price</td>
                </tr>
                <tr class="item">
                  <td>Website Design</td>
                  <td>$300.00</td>
                </tr>
                <tr class="item">
                  <td>Hosting (3 months)</td>
                  <td>$75.00</td>
                </tr>
                <tr class="item last">
                  <td>Domain Registration (1 year)</td>
                  <td>$10.00</td>
                </tr>
                <!-- Total -->
                <tr class="total">
                  <td></td>
                  <td>Total: $385.00</td>
                </tr>
              </table>
          </table>
        </div>
      </body>
      </html>
    `;
    
  }
```
:::

