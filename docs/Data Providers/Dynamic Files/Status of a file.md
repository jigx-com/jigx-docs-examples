---
title: Status of a file
slug: SmP5-update
createdAt: 2023-11-09T08:48:39.693Z
updatedAt: 2025-05-21T09:46:52.868Z
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example demonstrates how to track the upload status of a file and retry uploads for any that fail. The `_fileStatus` system table, along with the `expense` Dynamic Data table, are used as datasources to display upload progress.

Progress is shown in a `list-item` using `color`, `progress`, and a status `label`. If a file fails to upload, swipe left and use the `action.retry-queue-command` to attempt the upload again.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-C2z-QoO-_f4ZycKRz0uWo-20250521-115828.gif" size="66" position="center" caption="File status" alt="File status"}
:::
::::

:::CodeblockTabs
file-expense-create.jigx

```yaml
# Use this jig to upload a file. 
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

inputs:
  expenseId:
    type: string
    
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
        - type: component.text-field
          instanceId: fileName
          options:
            label: File name      
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
                method: create
                data:
                  id: =@ctx.jig.components.recordid.state.value
                  expenseitem: =@ctx.jig.components.expenseitem.state.value
                  expenseamount: =@ctx.components.expenseamount.state.value
                file: 
                  localPath: =@ctx.components.expenseimage.state.value
                  fileName: =@ctx.components.fileName.state.value
            # The file upload progress is shown in a new jig, 
            # use go-to action to navigate to the jig.
            # Provide the inputs for the file.    
            - type: action.go-to
              options:
                linkTo: expense-file-upload-status
                inputs: 
                  expenseId: =@ctx.jig.inputs.expenseId
                  fileName: =@ctx.components.fileName.state.value
```

expense-file-upload-status.jigx

```yaml
title: Expense file upload status
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2021/02/04/19/58/fabric-5982467_640.jpg
# The expenseId is used as an input to see the progress on the specific file.     
inputs:  
    expenseId:
      type: string
    fileName:
      type: string 
# Configure a datasource to use the _fileStatus table,
# to evaluate the upload status and the expense table that the file is
# associated with.       
datasources:
  file-status-ds:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - _fileStatus
        - default/expenses
      query: |
        SELECT
          e.id,
          '$.expenseId',
          e.timestamp,
          json_extract(e.file, '$.localPath') as localPath,
          json_extract(e.file, '$.fileName')  as fileName,
          fs.commandId as commandId,
          fs.progress as progress,
          fs.state as uploadstatus
        FROM [_fileStatus] AS fs
        LEFT JOIN [default/expenses] AS e ON
        e.id = fs.id
        ORDER BY e.timestamp
      queryParameters:
        expenseId: =@ctx.jig.inputs.expenseId
  
children:
  - type: component.form
    instanceId: expenseitem
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: name
          options:
            label: File name
            initialValue: =@ctx.jig.inputs.fileName
  # Configure a list-item to show the progress of the file upload,
  # with a color and percentage.         
  - type: component.list
    options:
      data: =@ctx.datasources.file-status-ds
      maximumItemsToRender: 20
      item: 
        type: component.list-item
        options:
          title: =@ctx.current.item.fileName
          color:
            - color: color11
              when: =(@ctx.current.item.progress >= 1)
            - color: color2
              when: =(@ctx.current.item.progress >= 75 and @ctx.current.item.progress < 100)
            - color: color1
              when: =(@ctx.current.item.progress < 75 and @ctx.current.item.progress > 30)
            - color: color8
              when: =(@ctx.current.item.progress <= 30)
          description: =@ctx.current.item.progress & '%'
          # Add a label to display the upload status.
          label:
            title: =@ctx.current.item.uploadstatus
          progress: >
            =@ctx.current.item.progress != null ? (@ctx.current.item.progress / 100) :
            0
          # Configure a swipeable action,
          # to allow a retry on any files that fail. 
          swipeable:
            left:
              - color: primary
                icon: pencil-2
                label: Retry
                onPress:
                  type: action.action-list
                  options:
                    isSequential: true
                    actions:
                      - type: action.retry-queue-command
                        options:
                          id: =@ctx.current.item.commandId
```
:::
