# open-media-picker

This action lets you immediately open the media picker, enabling you to capture images and videos or select media files, then output the selected files.

## Configuration options

| **Core structure** |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `title`            | Provide a short title to display on the action button. You can use text, an expression or a datasource to set the title.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `mediaType`        | By default the value is set to `image`. The following options are available for selection:&#xA;1\) `any` is for files of any extension such as pdf, jpeg, png, mpeg, txt, or docx. Set to `any` allows you to take a picture, record a video, select an image or video from the library, or select a document. Using `mediaType: any` is recommended when uploading multiple media files as it caters for any file type.&#xA;2\) `csv` - select CSV files.&#xA;3\) `doc` - select DOC or DOCX files.&#xA;4\) `image` - used to take a picture or select from the image library.&#xA;5\) `imageAndVideo` - take a picture, record a video or select an  image or video from the library.&#xA;6\) `pdf` - select PDF files.&#xA;7\) `plainText` - select plain text files.&#xA;8\) `ppt` - select PPT or PPTX files.&#xA;9\) `video` - record a video or upload one from the library.&#xA;10\) `xls` -  select XLS or XLSX files.&#xA;Configure filters to restrict media types based on your app’s requirements, for example, only allow document files DOC, PDF or plain text. &#xA;`mediaType:`&#xA;      `- doc`&#xA;      `- pdf` |

| **Other options** |                                                                                                                                                                                                                                                                                                                        |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `icon`            | Specify the [icon](#) to display on the action button. The icon only applies to `swipeable`, `secondary`, and [header](./../Components/jig-header.md) actions. Icon setups are not supported on primary actions.                                                                                                       |
| `imageCropping`   | You can set any of the following with `imageCropping` :&#xA;`isEnabled` - allows you to crop an image.&#xA;`height` - maximum allowed is 5000px.&#xA;`width`- maximum allowed is 5000px.&#xA;`isFreeStyleCropEnabled` - when set to `true` it supports custom cropping to change the size or aspect ratio of an image. |
| `imageQuality`    | Image quality after compression (from 0 to 100, where 100 is the best quality). On iOS, values larger than 80 don't produce a noticeable quality increase in most images, while a value of 80 will reduce the file size by about half or less compared to a value of 100. Default: 100 (Android)/ 80 (iOS).            |
| `isHidden`        | When set to `true` the action button is hidden.                                                                                                                                                                                                                                                                        |
| `isMultiple`      | Set to `true` allows for multiple files to be added or shown. Set to `false` allows for a single file.                                                                                                                                                                                                                 |
| `maximumFileSize` | `maximumFileSize =6 * 1024 * 1024` by default. Set the value to `none` if no size evaluations must be performed. File size format is in bytes. Applies to images and videos.                                                                                                                                           |
| `style`           | Add styling to the action button. More than one can be set to true, evaluation is based on priority. &#xA;- `isDanger` - Change the button style to error&#xA;- `isDisabled` - Disables the button preventing it from being tapped.&#xA;- `isPrimary` - Change style of the button to primary. Default is primary.     |

| **Outputs**                         | **Key**      | **Notes**                                                                         |
| ----------------------------------- | ------------ | --------------------------------------------------------------------------------- |
| `=@ctx.actions.instanceId.outputs.` | newItems     | string\[]&#xA;Used for newly added items that were successfully uploaded.         |
| `=@ctx.actions.instanceId.outputs.` | invalidItems | string\[]&#xA;Used for options that are invalid or failed to upload successfully. |

## Considerations

- Files captured using the `media-field` component can be saved to [Dynamic Files](<./../Data Providers/Dynamic Files.md>) by assigning them to the `file` property of a dynamic data entity, enabling seamless upload and storage in Amazon S3.

## Examples and code snippets

::::ExpandableHeading
### Open-media-picker to capture an image

In this example, the button opens the media-picker. The configuration is set to take a picture or choose from library. The image is saved to the local database.

![Action open media-picker](https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-a3B29qbky6oi4N7auiU5F-20250220-173914.png "Action open media-picker")

:::CodeblockTabs
action-open-media-picker.jigx

```yaml
title: Job details 
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: >
       https://images.unsplash.com/photo-1640682841767-cdfce3aea6e0
       ?w=800&auto=format&fit=crop&q=60&ixlib=rb-4.0.3
       &ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fHBsdW1iZXJ8ZW58MHx8MHx8fDA%3D

children:
  - type: component.form
    instanceId: form-details
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: job-number
          options:
            label: Job Number
        - type: component.text-field
          instanceId: job-notes
          options:
            isMultiline: true
            label: Add notes
        - type: component.checkbox
          instanceId: checklist
          options:
            icon: check
            color: positive
            label: Completed checklist?
        - type: component.date-picker
          instanceId: job-date
          options:
            label: Job date
actions:
  - children:
      - type: action.action-list
        options:
          title: Take a photo
          isSequential: true
          actions:
          # Add the media-picker action to open the media modal.
          - type: action.open-media-picker
            # Use an id that is used to reference
            # the action's output when saved as data.
            instanceId: job-photo
            options:
              # Specify the type of media required.
              mediaType: image
          # Use an action to save the images to a data provider.    
          - type: action.execute-entities
            options: 
              provider: DATA_PROVIDER_LOCAL
              method: save
              entity: local-images
              # Use the action's output to reference the image file.
              data: =@ctx.actions.job-photo.outputs      
```
:::
::::

