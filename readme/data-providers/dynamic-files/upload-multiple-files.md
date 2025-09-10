# Upload multiple files

### Introduction to Uploading Multiple Files

Uploading multiple files within a single operation can significantly enhance user experience and streamline data management processes. To achieve this, the `media-picker` component or the `open-media-picker` action is utilized for file selection. Once selected, the `execute-entities` action is used to upload these files to the Dynamic Files database. By leveraging the `$map` operation within both the `data` and `file` properties, a separate record is created for each file, ensuring organized and efficient data storage. This approach facilitates efficient handling of bulk file uploads while maintaining data integrity.

## Uploading multiple images using the media-field component

This example demonstrates a file upload form featuring a `media-field` component configured for multiple file selection and an `entity-field` for specifying filenames with extensions. It uses the `execute-entities` action to upload files to the Dynamic Files database. By utilizing the `$map` operation, each file is processed to create an individual record.

<figure><img src="../../../.gitbook/assets/DF-multiple-Upload-comp.png" alt="Uploading multiple files" width="563"><figcaption><p>Uploading multiple files</p></figcaption></figure>

{% code title="create-expense-receipt.jigx" %}
```yaml
title: Expense Claim/Receipts - Add 
type: jig.default
description: Expense

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://unsplash.com/photos/a-piece-of-paper-sitting-on-top-of-a-table-ClMubWJQgY0

onFocus:
  type: action.reset-state
  options:
    state: =@ctx.components.expense.state.data

actions:
  - numberOfVisibleActions: 1
    children:  
      # Use execute-entities to upload multiple files with $map to create a separate
      # record for each file.
      - type: action.execute-entities
        options:
          title: Save Entities
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/expensefiles
          method: create
          data: >
            =$map(@ctx.components.receiptMedia.state.value, function($v,
            $i, $a) {
              $.{
                "expenseId": @ctx.jig.inputs.expenseId,
                "comments": @ctx.components.fileName.state.value,
                "dateModified": $now()
                }
              })
          file: >
            =$map(@ctx.components.receiptMedia.state.value, function($v,
            $i, $a) {
              $.{
                "localPath": $v,
                "fileName": @ctx.components.fileName.state.value
                }
              })
          goBack: previous
 
children:
  - type: component.form
    instanceId: expense
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: recordid
          options:
            initialValue: =@ctx.jig.inputs.expenseId
            isHidden: true
            label: recordid

        - type: component.media-field
          instanceId: receiptMedia
          options:
            isMultiple: true
            label: Receipts
            maximumFileSize: =500 * 1024 * 1024
            mediaType: any

        - type: component.text-field
          instanceId: fileName
          options:
            helperText: Add an extension
            label: Uploaded file's path

  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: File
            value: =@ctx.components.receiptMedia.state.value

```
{% endcode %}

## Uploading multiple images using the open-media-picker

This example demonstrates a file upload form featuring a `open-media-picker` action configured for multiple file selection and an `entity-field` for specifying filenames with extensions. It uses the `execute-entities` action to upload files to the Dynamic Files database. By utilizing the `$map` operation, each file is processed to create an individual record.

<figure><img src="../../../.gitbook/assets/DF-multiple-upload-action.png" alt="Uploading multiple files using the open-media-picker action" width="563"><figcaption><p>Uploading multiple files using the open-media-picker action</p></figcaption></figure>

{% code title="create-expense-receipt-action.jigx" %}
```yaml
title: Expense Claim/Receipts - Add
type: jig.default
description: Expense

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1670261197418-40e922b570d2?q=80&w=1635&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
onFocus:
  type: action.reset-state
  options:
    state: =@ctx.components.expense.state.data

actions:
  - children:
      - type: action.action-list
        options:
          isSequential: true
          title: Upload Receipts
          actions:
            - type: action.open-media-picker
              instanceId: job-photo
              options:
                imageQuality: 10
                mediaType: any
                isMultiple: true
            - type: action.execute-entities
              options:
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/expensefiles
                method: create
                data: >
                  =$map(@ctx.actions.job-photo.outputs.newItems, function($v,
                  $i, $a) {
                    $.{
                      "expenseId": @ctx.jig.inputs.expenseId,
                      "comments": @ctx.components.fileName.state.value,
                      "dateModified": $now()
                      }
                    })
                file: >
                  =$map(@ctx.actions.job-photo.outputs.newItems, function($v,
                  $i, $a) {
                    $.{
                      "localPath": $v,
                      "fileName": @ctx.components.fileName.state.value
                      }
                    })
                onSuccess:
                  type: action.confirm
                  options:
                    isConfirmedAutomatically: false
                    onConfirmed:
                      type: action.go-back
                    modal:
                      title: Files uploaded successfully

children:
  - type: component.form
    instanceId: expense
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: recordid
          options:
            initialValue: =@ctx.jig.inputs.expenseId
            isHidden: true
            label: recordid

        - type: component.text-field
          instanceId: fileName
          options:
            helperText: Add an extension
            label: Uploaded file's path

```
{% endcode %}
