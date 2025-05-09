---
title: Update/Save a file
slug: jhbL-up
description: Learn how to update a file in OneDrive using {{JigxApp}} with this comprehensive document. Discover the necessary YAML properties, including fileName and entity, and explore the use of the media-field component for file uploading. 
createdAt: Mon May 29 2023 08:24:46 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Mar 05 2025 13:47:19 GMT+0000 (Coordinated Universal Time)
---

Files often change and need to be edited or updated with additional information; for example, team members can collaborate and edit and update a contract proposal. You can update an existing file in OneDrive from a solution in the Jigx App. Use the [media-field](./../../Components/form/media-field.md) component in a form to upload the updated file or image, then use the OneDrive Data Provider, its update or save method, and required properties. The existing file in OneDrive will be updated.

![Updating a file on OneDrive](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-sB7j0dnUHnFgwToSWpikS-20250305-134712.png "Updating a file on OneDrive")

## Properties

The following properties are required in the YAML:

- `file` - reference the physical file
- `fileName` - add the file name with the extension, e.g. Invoice.pdf
- `entity`- file path in OneDrive
- `tokenType` - OAuth token credentials name
- `method: update`

## Component

To upload a file use the `media-field` component to select the file. Use the `image`, or `any` property in the `media-field` component to specify the `mediaType`.

## Considerations

- When no `id` is provided, a new record is created if it is not a duplicate filename
- **Important:** When updating a file and changing the filename, if the new name is the same as an existing file name, the amended file is saved to the existing file with no warning that the file will be overwritten
- The filename is crucial in determining if the item must be saved/updated or whether a new file should be created
- When only updating the file, it uses the `id` and the `file` and then saves/updates as requested
- Any change to the filename executes a create method, even if the `id` is specified and a new file is added to OneDrive
- Updating/saving an existing file by only changing the file, saves the file against the original record
- Jigx recommends you build in logic using a `modal` to show a message that the file will be overwritten
- Using the `method: save` will create a new file if the filename does not exist, otherwise the save will function as an update method
- A delay or time lag of several minutes could be experienced when files are syncing between the device and OneDrive

## Code Example

The code below provides an example of a list of invoices in the `myfiles` directory of OneDrive. When selecting the file in the dropdown list, the file name is displayed and the media picker is used to uploade the updated file. Pressing the *Update Invoice* button updates the file on OneDrive.

:::CodeblockTabs
Update-file.jigx

```yaml
title: Update Invoice 
description: Update monthly invoices
type: jig.default

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://builder.jigx.com/assets/images/header.jpg
onFocus: 
  type: action.sync-entities
  options: 
    #use the OneDrive provider to sync the file metadata to the local provider
    provider: DATA_PROVIDER_ONEDRIVE
    entities:
      - entity: myfiles
        data: 
          tokenType: jigx.graph.oauth 

datasources:
  file-data-root: 
    options:
       provider: DATA_PROVIDER_LOCAL 
       entities: 
         - myfiles
       query: SELECT id, '$.name' as name, '$.file' FROM [myfiles] ORDER BY '$.name' DESC  
    type: datasource.sqlite

children: 
  - type: component.form
    instanceId: Invoices
    options:
      children: 
        - type: component.dropdown
          instanceId: SelectFile
          options:
            label: Select a file to update
            data: =@ctx.datasources.file-data-root
            item:
              type: component.dropdown-item
              instanceId: =@ctx.current.item.name
              options:
                title: =@ctx.current.item.name
                value: =@ctx.current.item.name
        - type: component.text-field
        # reference the required OneDrive fileName property as the instanceId 
          instanceId: FileName
          options:
            label: Invoice Name
            initialValue: =@ctx.components.SelectFile.state.selected.name
        - type: component.media-field
        # reference the required OneDrive file property as the instanceId 
          instanceId: File
          options:
            label:  Updated Invoice
            mediaType: any
          
actions:
  - children:
      - type: action.action-list
        options:
          title: Update Invoice
          isSequential: true
          actions:
             - type: action.confirm
               options:
                  isConfirmedAutomatically: =@ctx.components.FileName.state.value = @ctx.components.SelectFile.state.selected.name ? true:false
                  onConfirmed: 
                    type: action.execute-entity
                    options: 
                      # Use the OneDrive provider with the update method to update the file on OneDrive
                      provider: DATA_PROVIDER_ONEDRIVE
                      entity: myfiles
                      method: update
                      data: 
                      file: =@ctx.components.File.state.value
                      fileName: =@ctx.components.FileName.state.value
                      tokenType: jigx.graph.oauth 
                      id: =@ctx.components.SelectFile.state.selected.id
                      onSuccess: 
                        title: File successfully updated
                        
                  modal:
                    title: Changing the file name will create a new file (create method) 
             - type: action.go-back
```
:::

Example of a `modal` message that can be displayed when overwriting an existing file.

:::CodeblockTabs
Modal

```yaml
  modal:
    title:  This will overwrite the existing file, are you sure you want to proceed?
    cancel: Cancel 
    confirm: Error message      
```
:::

### See also

- [Microsoft OneDrive]()
- [Create a file](<./Create a file.md>)
- [Delete a file](<./Delete a file.md>)
- [List files](<./List files.md>)
- [Download a file](<./Download a file.md>)

