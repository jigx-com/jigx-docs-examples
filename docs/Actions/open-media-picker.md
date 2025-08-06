# open-media-picker

This action lets you immediately open the media picker, enabling you to capture images and videos or select media files, then output the selected files.

## Configuration options

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="118">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide a short title to display on the action button. You can use text, an expression or a datasource to set the title.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>mediaType</code></p>
    </td>
    <td selected="false" align="left">
      <p>By default the value is set to <code>image</code>. The following options are available for selection:
      1) <code>any</code> is for files of any extension such as pdf, jpeg, png, mpeg, txt, or docx. Set to <code>any</code> allows you to take a picture, record a video, select an image or video from the library, or select a document. Using <code>mediaType: any</code> is recommended when uploading multiple media files as it caters for any file type.
      2) <code>csv</code> - select CSV files.
      3) <code>doc</code> - select DOC or DOCX files.
      4) <code>image</code> - used to take a picture or select from the image library.
      5) <code>imageAndVideo</code> - take a picture, record a video or select an  image or video from the library.
      6) <code>pdf</code> - select PDF files.
      7) <code>plainText</code> - select plain text files.
      8) <code>ppt</code> - select PPT or PPTX files.
      9) <code>video</code> - record a video or upload one from the library.
      10) <code>xls</code> -  select XLS or XLSX files.
      Configure filters to restrict media types based on your app’s requirements, for example, only allow document files DOC, PDF or plain text.
      <code>mediaType:</code>
      <code>- doc</code>
      <code>- pdf</code></p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="164">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>icon</code></p>
    </td>
    <td selected="false" align="left">
      <p>Specify the  to display on the action button. The icon only applies to <code>swipeable</code>, <code>secondary</code>, and <a href="./../Components/jig-header.md">header</a> actions. Icon setups are not supported on primary actions.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>imageCropping</code></p>
    </td>
    <td selected="false" align="left">
      <p>You can set any of the following with <code>imageCropping</code> :</p>
      <ul>
      <li><code>isEnabled</code> - allows you to crop an image.</li>
      <li><code>height</code> - maximum allowed is 5000px.</li>
      <li><code>width</code>- maximum allowed is 5000px.</li>
      <li><code>isFreeStyleCropEnabled</code> - when set to <code>true</code> it supports custom cropping to change the size or aspect ratio of an image.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>imageQuality</code></p>
    </td>
    <td selected="false" align="left">
      <p>Image quality after compression (from 0 to 100, where 100 is the best quality). On iOS, values larger than 80 don't produce a noticeable quality increase in most images, while a value of 80 will reduce the file size by about half or less compared to a value of 100. Default: 100 (Android)/ 80 (iOS).</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isHidden</code></p>
    </td>
    <td selected="false" align="left">
      <p>When set to <code>true</code> the action button is hidden.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>isMultiple</code></p>
    </td>
    <td selected="false" align="left">
      <p>Set to <code>true</code> allows for multiple files to be added or shown. Set to <code>false</code> allows for a single file.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>maximumFileSize</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>maximumFileSize =6 * 1024 * 1024</code> by default. Set the value to <code>none</code> if no size evaluations must be performed. File size format is in bytes. Applies to images and videos.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>style</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add styling to the action button. More than one can be set to true, evaluation is based on priority. </p>
      <ul>
      <li><code>isDanger</code> - Change the button style to error</li>
      <li><code>isDisabled</code> - Disables the button preventing it from being tapped.</li>
      <li><code>isPrimary</code> - Change style of the button to primary. Default is primary.</li>
      </ul>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="319,109">
  <tr>
    <td selected="false" align="left">
      <p><strong>Outputs</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Key</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Notes</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.actions.instanceId.outputs.</code></p>
    </td>
    <td selected="false" align="left">
      <p>newItems</p>
    </td>
    <td selected="false" align="left">
      <p>string[]
      Used for newly added items that were successfully uploaded.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>=@ctx.actions.instanceId.outputs.</code></p>
    </td>
    <td selected="false" align="left">
      <p>invalidItems</p>
    </td>
    <td selected="false" align="left">
      <p>string[]
      Used for options that are invalid or failed to upload successfully.</p>
    </td>
  </tr>
</table>

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

