# Delete a file

## Delete a file in a jig

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, a list of expenses is displayed with the following:

- The `subtitle` displays the `filename`.
- A `label` is configured with `color` and text to display the status of the file.
- A `left swipeable` action is configured with two actions:
  - The first only deletes the file associated with the record using the `execute-entity` action with the `update` method and the file property set to `null`.
  - The second deletes the entire record in the database using the `execute-entity` action with the `delete` method.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-JG8sn10_wFTyXLGp_QSAS-20250519-125130.gif" size="66" position="center" caption="Delete record or file" alt="Delete record or file" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-JG8sn10_wFTyXLGp_QSAS-20250519-125130.gif"}
:::
::::

:::CodeblockTabs
file-expense-list.jigx

```yaml
title: Expense Categories
description: List of Expenses
type: jig.list
icon: bill-cross-money-clipboard

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2023/08/22/11/57/finance-8206242_1280.jpg

data: =@ctx.datasources.expenses-ds
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.expenseitem
    # Configure the subtitle to display the document filename.
    subtitle: =@ctx.current.item.filename
    # Use the label to show the status of the file,
    # as shown in the file metadata. 
    label:
      color:
        - when: =@ctx.current.item.status = 'UPLOADED'
          color: color2
        - when: =@ctx.current.item.status = 'PENDING'
          color: primary
        - when: =@ctx.current.item.status = 'PROCESSING'
          color: color3
      title: =@ctx.current.item.status
    leftElement:
      # Configure a left avatar int he list to display the file thumbnail.
      element: avatar
      text: ""
      uri: |
        =@ctx.current.item.thumbnail != null ? 'data:image/png;base64,' & @ctx.current.item.thumbnail :
        @ctx.current.item.localPath != null ? @ctx.current.item.localPath
   # Configure a left swipeable action with two actions, 
   # the first deletes the entire record in the database.
   # The second only deletes the file associated with the record.      
    swipeable:
      left:
        - label: Delete expense
          icon: delete-2
          color: negative
          onPress: 
            # First action deleting entire record.
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/expenses
              method: delete
              goBack: stay
              data:
                id: =@ctx.current.item.id
        - label: Delete receipt
          icon: bin-2-alternate
          color: warning
          onPress: 
            # Second action only deletes the file. 
            # The records still exists. 
            type: action.execute-entity
            options:
              provider: DATA_PROVIDER_DYNAMIC
              entity: default/expenses
              method: update
              goBack: stay
              data:
                id: =@ctx.current.item.id
              file: null
# Action configured to go to the create expense jig, 
# where a file can be uploaded.            
actions:
  - children:
      - type: action.go-to
        options:
          title: Create Expense
          linkTo: files-create-expense    
```

datasource

```yaml
datasources:
  expenses-ds:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/expenses
      query: |
        SELECT
          id,
          '$.expenseitem',
          json_extract(file, '$.localPath') as localPath,
          json_extract(file, '$.fileName')  as filename,
          json_extract(file, '$.status') as status,
          json_extract(file, '$.thumbnail.base64') as thumbnail
        FROM [default/expenses]
        ORDER BY '$.expenseitem'
```
:::

In Management the *Hotel accomodation* record is deleted in the **expense** dynamic data table and the *airplane ticket* file is deleted but the record still exists.

## Delete a file in Jigx Management

Files can be deleted in Management by following these steps:

1. Log in to [https://manage.jigx.com](https://manage.jigx.com).
2. Browse to the required solution's **data** tab and select the record containing the file to be deleted.
3. Select the **File** tab, and click the **x** next to file's thumbnail.
   **Caution:** Clicking the *Delete* button at the bottom of the Edit record pane deletes the entire record and file.

