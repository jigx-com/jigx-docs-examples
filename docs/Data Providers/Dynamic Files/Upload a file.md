# Upload a file

## Upload file in a jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, an expense claim form allows you to capture expense details and upload a file, such as a slip or invoice.

The `media-field` is configured to accept `any` file type, with a `maximumFileSize` set to ensure files remain within acceptable limits. An `execute-entity` action creates the record in the datasource and links the uploaded file to the record by using the `create `method, with the `file` specified in the `localPath` property.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-uCb0bqIVvxwoDdMihP0My-20250519-074426.gif" size="66" position="center" caption="Upload file" alt="Upload file" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-uCb0bqIVvxwoDdMihP0My-20250519-074426.gif"}
:::
::::

:::CodeblockTabs
file-create-expense.jigx

```yaml
title: Expense Claim
description: Expense
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2016/05/04/23/02/receipts-1372960_1280.jpg

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.components.expense.state.data

children:
  - type: component.form
    instanceId: expense
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: recordid
          options:
            label: recordid
            isHidden: true
            initialValue: =$uuid()
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: expenseitem
                options:
                  label: Expense detail
              - type: component.number-field
                instanceId: expenseamount
                options:
                  label: Amount
                  format:
                    numberStyle: currency
                    currency: USD
        # Use the media field to select the file to be uploaded.           
        - type: component.media-field
          instanceId: expenseimage
          options:
            label: Expense receipt
            mediaType: any
            maximumFileSize: =500 * 1024 * 1024
            isMultiple: false

actions:
  - children:
      - type: action.action-list
        options:
          title: Submit
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/expenses
                # Configure the create method with a file property,
                # the file will be linked to the record.
                method: create
                goBack: previous
                data:
                  id: =@ctx.jig.components.recordid.state.value
                  expenseitem: =@ctx.jig.components.expenseitem.state.value
                  expenseamount: =@ctx.components.expenseamount.state.value
                file: 
                  localPath: =@ctx.components.expenseimage.state.value
```
:::

In Management the record is created in the **expense** dynamic data table and the file is linked to the record. The file and metadata is displayed in the file tab of the record. The file thumbnail is displayed in the system file column (use column settings to set the column to visible).

![Files in Management](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY--_meerV3mLUQB6DlK4OWi-20250519-075245.gif "Files in Management")

## Upload a file in Jigx Management

Files can be uploaded in Management by following these steps:

1. Log in to [https://manage.jigx.com](https://manage.jigx.com).
2. Browse to the required solution's **data** tab and select the record you want to add a file too, or create a new record.
3. Select the **File** tab, and add the file.
4. Add a **Name** for the file and include the file extension. If no file name is specified the name of the file is used.
5. Click the **Save** button.
6. The **status** of the file upload is shown in the top left corner of the File tab.

