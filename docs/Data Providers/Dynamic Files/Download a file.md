# Download a file

## Download a file in jig

{% columns %}
{% column %}
This example displays a department's expenses in a list. The expense receipt is downloaded by tapping the button to the right of the expense. A jig opens, displaying the receipt and its metadata. To `download` the receipt to a `localPath`, the `execute-entity`'s `download` method is configured. A `go-to` action opens a jig that displays the downloaded file in an `image` component and the file's metadata in `entity-fields`.
{% endcolumn %}

{% column %}
<figure><img src="../../../.gitbook/assets/DF-download-file.gif" alt="" width="170"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="file-download-receipts.jigx" %}
{% code fullWidth="true" %}
```yaml
title: Department Expense list
description: List of Expenses
type: jig.list

inputs:
  expenseId:
    type: string 
    
header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://cdn.pixabay.com/photo/2023/08/22/11/57/finance-8206242_1280.jpg
# The datasource allows you to use the thumbnail image URI from the server, 
# for faster loading and lower bandwidth.
# The full image for high-resolution, detailed viewing or editing.
# The image is stored in the cache (localPath) to cater for offline use,
# and repeated requests for the same image. 
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

data: =@ctx.datasources.expenses-ds
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.expenseitem
    subtitle: =@ctx.current.item.filename 
    tags:
      - text: =@ctx.current.item.status
        color: color14  
    leftElement:
      element: avatar
      text: ""
      uri: |
        =@ctx.current.item.thumbnail != null ? 'data:image/png;base64,' & @ctx.current.item.thumbnail :
        @ctx.current.item.localPath != null ? @ctx.current.item.localPath
    rightElement: 
      element: button
      title: View receipt
      onPress: 
        type: action.action-list
        options:
          isSequential: true
          actions:
            # Configure the download method to download the file,
            # to a local cache, use the current item's id.
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/expenses
                method: download
                data:
                    id: =@ctx.current.item.id
            # Configure a go-to action to view the file and file metadata.        
            - type: action.go-to
              options:
                linkTo: expense-receipt-details
                inputs: 
                  expenseId: =@ctx.current.item.id
            
actions:
  - children:
      - type: action.go-to
        options:
          title: Create Expense
          linkTo: files-create-expense
```
{% endcode %}
{% endtab %}

{% tab title="expense-receipt-details.jigx" %}
{% code fullWidth="true" %}
```yaml
title: Receipt Details
type: jig.default

inputs:
  expenseId:
    type: string  

datasources:
  receipt-ds:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/expenses
      query: |
        SELECT
          id,
          '$.expenseitem',
          '$.comments',
          json_extract(file, '$.localPath') as localPath,
          json_extract(file, '$.fileName')  as fileName,
          json_extract(file, '$.filepath')  as filepath,
          json_extract(file, '$.contentType') as contentType,
          json_extract(file, '$.contentLength') as contentLength,
          json_extract(file, '$.thumbnail.base64') as thumbnailBase64,
          json_extract(file, '$.thumbnail.contentType') as thumbnailContentType,
          json_extract(file, '$.thumbnail.contentLength') as thumbnailContentLength
        FROM [default/expenses]
        WHERE id = @expenseId
      queryParameters:
        expenseId: =@ctx.jig.inputs.expenseId
children:  
  # Configure the image component to use the localpath,
  # to display the downloaded file.      
  - type: component.image
    options:
      source:
        uri: =@ctx.datasources.receipt-ds.localPath
  # Configure entity fields to view the file metadata.  
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: filename
            value: =@ctx.datasources.receipt-ds.fileName
        - type: component.entity-field
          options:
            label: contentLength
            value: =@ctx.datasources.receipt-ds.contentLength
        - type: component.entity-field
          options:
            label: contentType
            value: =@ctx.datasources.receipt-ds.contentType
        - type: component.entity-field
          options:
            label: localPath
            value: =@ctx.datasources.receipt-ds.localPath
        - type: component.entity-field
          options:
            label: thumbnailContentLength
            value: =@ctx.datasources.receipt-ds.thumbnailContentLength
        - type: component.entity-field
          options:
            label: thumbnailContentType
            value: =@ctx.datasources.receipt-ds.thumbnailContentType
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Downloading multiple files

In scenarios where multiple files must be downloaded, use the `execute-entities` action. In the `data` property, configure an expression using the `$map` JSONATA [Path Operators](<Download a file.md>) to handle multiple entries.

{% code title="download-multiple-files" fullWidth="true" %}
```yaml
 actions:
  - children:
      # Configure the execute-entities for multiple file downloads.
      - type: action.execute-entities
        options:
          title: Download All
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/expenses
          # Use the download method. 
          method: download
          # Configure the data using the map path operator,
          # to download multiple files.
          data: |
            =$map(@ctx.datasources.receipt-ds.id, function($v, $i, $a) {
              $.{
                "id": $v
                }
              })
```
{% endcode %}

## Download a file in Jigx Management

Files can be uploaded in Management by following these steps:

1. Log in to [https://manage.jigx.com](https://manage.jigx.com).
2. Browse to the required solution's **data** tab and select the record containing the file to be downloaded.
3. Select the **File** tab in the Edit record pane.
4. To download the file use the **Download file** link at the top of the record.
