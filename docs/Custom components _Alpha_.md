---
title: Custom components (Alpha)
slug: OVPG-custom
createdAt: Mon Jun 12 2023 12:15:24 GMT+0000 (Coordinated Universal Time)
updatedAt: Tue Apr 22 2025 11:32:50 GMT+0000 (Coordinated Universal Time)
description: >-
  Learn about custom components in Jigx, which enhance the standard UI
  capabilities. Discover why and when to use custom components, and get a
  step-by-step guide on creating and reusing them in Jig. Exp
---

# Custom components (Alpha)

:::hint{type="danger"} This feature is currently in its **Alpha** stage of development.

* As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
* In this phase, the feature may contain bugs or behave unpredictably.
* Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
* We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases. :::

Custom components extend the standard set of components in Jigx to provide additional UI capabilities and features. To understand what custom components are, when and why you would use them, see [Custom Components (Alpha)](https://docs.jigx.com/custom-components-alpha).

1. [Creating custom components (Alpha)](https://docs.jigx.com/creating-custom-components-alpha) explains where and how to create the components and how to reuse them in a jig.
2. Passing data in and out of custom components is explained in [Inputs & outputs (Alpha)](https://docs.jigx.com/inputs-and-outputs-alpha).
3. [Combine custom & standard components (Alpha)](<Custom components _Alpha_/Combine custom _ standard components _Alpha_.md>) to create your own customized components and templates.
4. Jigx offers a variety of [Templates (Alpha)](<Custom components _Alpha_/Templates _Alpha_.md>) ready to use in your app, making development faster and easier. Select the template you want to use, copy the code from GitHub, and customize it to meet your needs.
5. The components that fall into the custom component category are:
   1. [Button (Alpha)](<Custom components _Alpha_/Button _Alpha_.md>)
   2. [Card (Alpha)](<Custom components _Alpha_/Card _Alpha_.md>)
   3. [Icon (Alpha)](<Custom components _Alpha_/Icon _Alpha_.md>)
   4. [Text (Alpha)](<Custom components _Alpha_/Text _Alpha_.md>)
   5. [View (Alpha)](<Custom components _Alpha_/View _Alpha_.md>)

### How to create a custom component

::::WorkflowBlock :::WorkflowBlockItem In Jigx Builder in the components folder, create a new jigx file, e.g., custom-button.jigx. :::

:::WorkflowBlockItem Select the `type: component.default`. All custom components require this type. :::

:::WorkflowBlockItem Under the `children:` property, use IntelliSence (Ctrl+space) to see the list of available components. Select the components, e.g., `type: component.button`. :::

:::WorkflowBlockItem Under the `options:` properties, create a space and use **ctrl+space** to open the IntelliSense popup\*\*.\*\* :::

:::WorkflowBlockItem You can select the styling properties from the list shown. :::

:::WorkflowBlockItem Configure the other properties provided in the code snippet. :::

:::WorkflowBlockItem Open the jig where you want to use the custom component and reference `component.custom-component`. Use the `componentId` property to reference the name of the custom component file, e.g., `componentId: custom-button`. :::

:::WorkflowBlockItem Test the jig on a mobile device to ensure the button is rendering correctly. ::: ::::

### Considerations

* [Localization](https://docs.jigx.com/localization) can be applied to custom components such as [Button (Alpha)](<Custom components _Alpha_/Button _Alpha_.md>) and [Text (Alpha)](<Custom components _Alpha_/Text _Alpha_.md>).
*   You can nest custom components by using `component.custom-component` and referencing the desired component in the `componentId` property.

    ```yaml
    type: component.default
    componentId: brand-form

    children:
      # Reference a custom component inside this custom component using componentId.
      - type: component.custom-component
        componentId: itinerary-day
      - type: component.card
        options:
          children:
            - type: component.form
              instanceId: new-form
              options:
                children:
                  - type: component.text-field
                    instanceId: company-name
                    options:
                      label: Company Name
    ```
* When using `component.image` in a custom component, the `height` property must be specified as part of the `size` property, otherwise validation errors occur, see below:

:::CodeblockTabs Correct YAML

```yaml
# Correct YAML snippet for using the height property in the image component,
# when used in a custom component.
- type: component.image
          options:
            size:
              height: 196
            source:
              uri: https://images
```

Incorrect YAML

```yaml
# Incorrect YAML snippet for using the height property in the image component,
# when used in a custom component.
- type: component.image
          options:
            height: 196
            source:
              uri: https://images
```

:::

{% code title="TEST CODE" lineNumbers="true" fullWidth="true" %}
```yaml
title: Add New Files
type: jig.default

actions:
  - children:
      - options:
          title: Upload Files
          actions:
            - type: action.execute-entities
              when: =$count(@ctx.datasources.fileInfo) > 0
              options:
                provider: DATA_PROVIDER_LOCAL
                entity: fileUrls
                data:
                  id: =@ctx.datasources.fileInfo.id
                goBack: stay
                method: delete
              
              
            - type: action.execute-entities
              options:
                provider: DATA_PROVIDER_REST
                entity: fileUrls
                data: >
                  =$map(@ctx.components.lMedia.state.value, function($item){
                            {
                              "filepath": $boolean(@ctx.components.frmFolder.state.value)? 
                                @ctx.components.frmFolder.state.value & "/" & $decodeUrlComponent($split($item, "/")[-1]) 
                                : $decodeUrlComponent($split($item, "/")[-1]),
                              "localFilePath": $item,
                              "contentType": @ctx.datasources.mimeTypes[fileExt = "." & $split($decodeUrlComponent($split($item, "/")[-1]), ".")[-1]].mimeType,
                              "localFileId": $uuid()
                            }
                          })[]
                function: get-file-upload-url
                functionParameters:
                  accessToken: jigx
                  contentType: application/vnd.openxmlformats-officedocument.wordprocessingml.document
                  orgId: 11111112-2dbe-4687-b98c-09b01c039743
                  solId: =@ctx.solution.id
                  ## the 3x parameters were missing
                  filepath: application/vnd.openxmlformats-officedocument.wordprocessingml.document
                  localFileId: application/vnd.openxmlformats-officedocument.wordprocessingml.document
                  localFilePath: application/vnd.openxmlformats-officedocument.wordprocessingml.document
                goBack: stay
                method: create
              
            - type: action.execute-entities
              options:
                provider: DATA_PROVIDER_REST
                entity: fileUrls
                ## function param was missing
                functionParameters:
                  file: =@ctx.datasources.fileInfo.url
                  url: =$decodeUrlComponent(@ctx.datasources.fileInfo.localFilePath)
                data: |
                  =$map(@ctx.datasources.fileInfo, function($item){
                    {
                      "url": $item.url,
                      "file": $decodeUrlComponent($item.localFilePath)
                    }
                  })[]
                function: upload-files
                goBack: previous
                method: functionCall
              
          isSequential: true
        type: action.action-list
        
datasources:
  fileInfo:
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: fileUrls
      query: |
        SELECT tbl.id as id, 
              json_extract(tbl.data, '$.accessToken') as accessToken, 
              json_extract(tbl.data, '$.filepath') as filepath, 
              json_extract(tbl.data, '$.localFileId') as localFileId, 
              json_extract(tbl.data, '$.localFilePath') as localFilePath, 
              json_extract(tbl.data, '$.orgId') as orgId, 
              json_extract(tbl.data, '$.solId') as solId, 
              json_extract(tbl.data, '$.contentType') as contentType, 
              json_extract(tbl.data, '$.id') as fileId, 
              json_extract(tbl.data, '$.url') as url, 
              json_extract(tbl.data, '$.expiry') as expiry 
        FROM [fileUrls] AS tbl
    type: datasource.sqlite
  mimeTypes:
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/mimeTypes
      query: |
        SELECT
        json_extract(fid.data, '$.fileExt') AS fileExt,
        json_extract(fid.data, '$.mimeType') AS mimeType
        FROM [default/mimeTypes] AS fid
    type: datasource.sqlite
children:
  - instanceId: frmFiles
    options:
      children:
        - instanceId: frmFolder
          options:
            label: DD Cloud Folder
          type: component.text-field
        - instanceId: fileName
          options:
            label: File Name
            textArea: large
            value: >
              =$string($map(@ctx.components.lMedia.state.value, function($item){
                        {
                          "filepath": $boolean(@ctx.components.frmFolder.state.value)? 
                            @ctx.components.frmFolder.state.value & "/" & $decodeUrlComponent($split($item, "/")[-1]) 
                            : $decodeUrlComponent($split($item, "/")[-1]),
                          "localFilePath": $item,
                          "contentType": @ctx.datasources.mimeTypes[fileExt = "." & $split($decodeUrlComponent($split($item, "/")[-1]), ".")[-1]].mimeType,
                          "localFileId": $uuid()
                        }
                      })[])
          type: component.text-field
        - instanceId: debug
          options:
            label: debug
          type: component.text-field
        - instanceId: lMedia
          options:
            isMultiple: true
            label: Files
            mediaType: any
          type: component.media-field
      isDiscardChangesAlertEnabled: false
    type: component.form
header:
  options:
    children:
      options:
        source:
          uri: https://builder.jigx.com/assets/images/header.jpg
      type: component.image
    height: small
  type: component.jig-header
onFocus:
  options:
    state: =@ctx.components.frmFiles.state.data
  type: action.reset-state

```
{% endcode %}
