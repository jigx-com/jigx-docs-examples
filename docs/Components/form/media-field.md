---
title: media-field
slug: klbu-media-field
description: Learn how to use the "media-field" component to easily upload files or take pictures using your device's camera. This document outlines the component's configuration options, including label settings, media type customization, file size limits, and image 
createdAt: Mon Jul 04 2022 09:02:26 GMT+0000 (Coordinated Universal Time)
updatedAt: Wed Apr 30 2025 11:02:40 GMT+0000 (Coordinated Universal Time)
---

This component uploads files, images, videos, or a combination of them. You can use saved files from your device or your camera to take pictures and videos.&#x20;

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9lqiAt-zCd9uHw6kf7fYT_cc-media-intro.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9lqiAt-zCd9uHw6kf7fYT_cc-media-intro.png" size="90" width="5098" height="2554" position="center" caption="Media Field Preview" alt="Media Field Preview"}

:::hint{type="warning"}
- `media-field` can only be used in [jig.default](<./../../Jig Types/jig_default.md>) or inside a [form](./../form.md) component.
- The `media-field` requires a data source to store the files, you can configure one of the [Data Providers](<./../../Data Providers.md>) for this.
- [Conversions]() allow you to determine the format the files are stored in and  returned in.
- Jigx does not recommend storing images in Dynamic Data (via any conversion), as the max file size per record is 350K.
:::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| ### Core structure | ****                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `instanceId`       | Provide an id for the media-field component.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `label`            | Label is displayed as a placeholder if there is no value provided. Use this property to provide a value that will guide the user to identify what must be uploaded, such as `Upload file` or `Upload a video`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `mediaType`        | By default the value is set to `image`. The following options are available for selection:<br />1) `any` is for files of any extension such as pdf, jpeg, png, mpeg, txt, or docx. Set to `any` allows you to take a picture, record a video, select an image or video from the library, or select a document. Using `mediaType: any` is recommended when uploading multiple media files as it caters for any file type.
2) `csv` - select CSV files.
3) `doc` - select DOC or DOCX files.
4) `image` - used to take a picture or select from the image library.
5) `imageAndVideo` - take a picture, record a video or select an  image or video from the library.
6) `pdf` - select PDF files.
7) `plainText` - select plain text files.
8) `ppt` - select PPT or PPTX files.
9) `video` - record a video or upload one from the library.
10) `xls` -  select XLS or XLSX files.<br />Configure filters to restrict media types based on your app’s requirements, for example, only allow document files DOC, PDF or plain text. See the *Restrict or filter the upload of media file types* code example below.  |

| ### Other options |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `intialValue`     | The `initialValue` loads and displays the configured media in the media-field when the form is initially loaded. You can use this property to preset the field with default media so that you do not have to manually select it. To change the intialValue simply tap the media-field and upload a new set of media. Using the `reset-state` action with `initialValues` does not clear the media-field, it resets the field back to it's `initialValue`.  |
| `imageCropping`   | You can set any of the following with `imageCropping` :&#xA;`isEnabled` - allows you to crop an image.&#xA;`height` - maximum allowed is 5000px.&#xA;`width`- maximum allowed is 5000px.&#xA;`isFreeStyleCropEnabled` - when set to `true` it supports custom cropping to change the size or aspect ratio of an image.                                                                                                                                     |
| `imageQuality`    | Image quality after compression (from 0 to 100, where 100 is the best quality). On iOS, values larger than 80 don't produce a noticeable quality increase in most images, while a value of 80 will reduce the file size by about half or less compared to a value of 100. Default: 100 (Android)/ 80 (iOS).                                                                                                                                                |
| `isMultiple`      | Set to `true` allows for multiple file to be added. Set to `false` allows for a single file.                                                                                                                                                                                                                                                                                                                                                               |
| `maximumFileSize` | `maximumFileSize =6 * 1024 * 1024` by default. Set the value to `none` if no size evaluations must be performed. File size format is in bytes. Applies to images and videos.                                                                                                                                                                                                                                                                               |

| ### Actions                | ****                                                                                                                                                                                                                                                                         |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `action.open-media-picker` | Configure the [open-media-picker](./../../Actions/open-media-picker.md) action that either immediately opens the device camera, allowing you to tap the action button on the screen to take an image or video, or allow you to select media files and output selected paths. |

## Considerations

- To delete a media file, click on the trash icon shown on the media thumbnail at the bottom of the selection screen.&#x20;
- When multiple files are selected the first thumbnail displays the trash icon. Tap on the image thumbnail you want to delete, the trash icon will display, tap on the icon, the image is deleted.
- An image, video, or file can be reference for upload from a data source.
- When using the `intialValue` property to display a media file be aware that uploading media from Android and trying to read it in iOS and vice versus is not possible as it cannot display the image due to the local-uri path. When a media-file cannot be viewed an icon with the file's title is displayed. Use [conversions ]() to base64 to store files.
- When uploading multiple files, by default only three files are displayed in the media-field. If there are more than three files for upload the third file is overlayed with a + and the number of files, e.g. +2 and the number of items displays in the top right-hand corner of the media-field.&#x20;

## Examples and code snippets ****

### Upload image & use freestyle cropping

This component *uploads* an image using the `mediaType: image` property. Clicking on the paperclip icon will display a menu where you can choose to upload an existing file from your device or use the camera to take a new image. After selecting the file, or loading and cropping the image to the specified size, the file is first validated, then the upload button becomes enabled.  Press the *Upload file *button at the bottom, which will trigger an action to *create* the file.&#x20;

**Examples:
**See the full example using dynamic data in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/media-field/media-field-image.jigx" target="_blank">GitHub</a>.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/u4A9URQ_qy9wPyxCLyr8E_cc-media-image-dd.png" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/u4A9URQ_qy9wPyxCLyr8E_cc-media-image-dd.png" size="90" width="3812" height="2524" position="center" caption="Image upload" alt="Image upload"}

:::CodeblockTabs
media-field (dynamic)

```yaml
title: Media field image upload
type: jig.default
icon: image-document-jpg
   
children:
  - type: component.form
    instanceId: media-form
    options:
      children:
        - type: component.media-field
          instanceId: media-field
          options:
            mediaType: image
            label: Upload image
            maximumFileSize: none
            imageCropping:
              width: 500
              height: 450
              isFreeStyleCropEnabled: true

actions:
  - children:
  # Media field requires an action to be uploaded. 
  # For this example we upload to the local data provider.
      - type: action.execute-entity
        options:
          title: Upload file
          provider: DATA_PROVIDER_LOCAL # you can use other data stores, e.g. REST data provider
          entity: products
          method: create
          data:
            image: =@ctx.components.media-field.state.value
            createdby: =@ctx.user.displayName
            createDate: =$now()    
          onSuccess: 
            type: action.go-back     
```
:::

### Upload multiple files

In this example we set the `isMultiple` property to `true` which allows for the selection of multiple files to be uploaded and `MediaType` to `any` which caters for images, videos and documents. The selected images display thumbnails at the bottom of the screen. Delete an image by pressing on the thumbnail until the trash icon appears then tap the icon and the image is deleted.&#x20;

![Upload multiple images](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/oaYhaIJ5ncX7ExpSidTus_cc-media-intro.png "Upload multiple images")

:::CodeblockTabs
mulitple-files-mediafield.jigx

```yaml
title: The Hiker's Diary Capturing Nature's Wonders
type: jig.default
icon: landmark-mountain

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1682687219640-b3f11f4b7234?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

datasources:
  hike-photos: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
  
      entities:
        - default/hike
  
      query: SELECT id, '$.name', '$.cotact', '$.scenery' FROM [default/hike] 
     
children:
  - type: component.form
    instanceId: hike-multiple
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.media-field
          instanceId: scenery
          options:
# Set media field to allow multiple image uploads         
            isMultiple: true
            label: Capture your hike 
            mediaType: image
           
actions:
  - children:
      - type: action.execute-entity
        options:
          title: Save photos
          provider: DATA_PROVIDER_DYNAMIC
          entity: default/hike
          method: create
          data:
            scenery: =@ctx.components.scenery.state.value
          onSuccess: 
            type: action.go-back  
```
:::

### Upload video

In this example multiple videos are uploaded, using the `mediaType: video` and `isMultiple: true` properties.  Select videos from the library or record videos to be uploaded. Tap the + icon in the bottom left corner to add multiple videos. The `execute-enitity` action uploads the videos and the metadata configured under `data` to the required data source.

**Example:
**See the example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/media-field/media-field-video.jigx" target="_blank">GitHub</a>.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/LqyGHS5xG4-ZTQdtlHy6z_cc-media-field-video.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/LqyGHS5xG4-ZTQdtlHy6z_cc-media-field-video.PNG" size="80" width="3822" height="2544" position="center" caption="Media-field upload videos" alt="Media-field upload videos"}

:::CodeblockTabs
media-field-video.jigx

```yaml
title: Media field video upload
type: jig.default
icon: image-document-jpg

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1485846234645-a62644f84728?q=80&w=2659&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
children:
  - type: component.form
    instanceId: media-form
    options:
      children:
        - type: component.text-field
          instanceId: video-info
          options:
            label: Description       
        - type: component.media-field
          instanceId: media-video
          options:
            mediaType: video
            label: Upload your location videos
            isMultiple: true

actions:
  - children:
  # Media field requires an action to be uploaded. 
  # For this example we upload to the local data provider, 
      - type: action.execute-entity
        options:
          title: Upload
          provider: DATA_PROVIDER_LOCAL # you can use other data stores, e.g. REST data provider
          entity: products
          method: create
          data:
            image: =@ctx.components.media-video.state.value
            createdby: =@ctx.user.displayName
            createDate: =$now()
          onSuccess: 
            type: action.go-back
```
:::

### Upload image or video

In this example multiple images and videos are uploaded, using the `mediaType: imageAndVideo` and `isMultiple: true` properties.  Select images and videos from the library, take a picture or record videos to be uploaded. Tap the + icon in the bottom left corner to add multiple images and videos. The `execute-enitity` action uploads the videos and metadata to the required data source.

**Example:
**See the example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/media-field/media-field-image-video.jigx" target="_blank">GitHub</a>.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3eTgQfZQG7HF4PAfFPYL2_cc-media-field-imgvideo.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/3eTgQfZQG7HF4PAfFPYL2_cc-media-field-imgvideo.PNG" size="66" width="2540" height="2500" position="center" caption="Media-field image and video" alt="Media-field image and video"}

:::CodeblockTabs
media-field-image-video.jigx

```yaml
title: Media field image or video upload
type: jig.default
icon: image-document-jpg

header:
  type: component.jig-header
  options:
    height: small
    children: 
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1523805009345-7448845a9e53?q=80&w=2672&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.form
    instanceId: media-form
    options:
      children:
        - type: component.text-field
          instanceId: media
          options:
            label: Share your experience with us
        - type: component.date-picker
          instanceId: date-visted
          options:
            label: Date visited
        - type: component.media-field
          instanceId: media-mixed
          options:
            mediaType: imageAndVideo
            label: Upload your location videos
            isMultiple: true

actions:
  - children:
  # Media field requires an action to be uploaded. 
  # For this example we upload to the local data provider, 
      - type: action.execute-entity
        options:
          title: Upload
          provider: DATA_PROVIDER_LOCAL # you can use other data stores, e.g. REST data provider
          entity: products
          method: create
          data:
            image: =@ctx.components.media-mixed.state.value.state.value
            createdby: =@ctx.user.displayName
            createDate: =$now()
          onSuccess: 
            type: action.go-back
```
:::

### Upload any files

In this example multiple files are uploaded for a claim, using the `mediaType: any` and `isMultiple: true` properties.  Select images, videos or documents from the library, take a picture or record videos related to the claim. Tap the + icon in the bottom left corner to add multiple files. The `execute-entity` action uploads the files and metadata to the required data source.

**Example:
**See the example in <a href="https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/media-field/media-field-any.jigx" target="_blank">GitHub</a>.

![Media-field upload any file](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jF5e6AKInY-z6OPDGebyh_cc-media-any.png "Media-field upload any file")

:::CodeblockTabs
media-field-any

```yaml
title: Media field any file upload
type: jig.default
icon: image-document-jpg

header:
   type: component.jig-header
   options:
     height: medium
     children: 
       type: component.image
       options:
         source:
           uri: https://plus.unsplash.com/premium_photo-1661370367221-982fdba4ce89?q=80&w=2671&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
       
children:
  - type: component.form
    instanceId: media-form
    options:
      children:
        - type: component.text-field
          instanceId: video-info
          options:
            label: Claim reference number
        - type: component.media-field
          instanceId: media-field
          options:
            mediaType: any
            label: Submit your claim documents
            maximumFileSize: none
            imageCropping:
              width: 500
              height: 450
              isFreeStyleCropEnabled: true
            isMultiple: true

actions:
  - children:
  # Media field requires an action to be uploaded. 
  # For this example we upload to the local data provider, you can use other data stores, e.g. REST data provider
       - type: action.execute-entity
        options:
          title: Submit claim
          provider: DATA_PROVIDER_LOCAL
          entity: products
          method: create
          data:
            image: =@ctx.components.media-field.state.value
            createdby: =@ctx.user.displayName
            createDate: =$now()
          onSuccess: 
            type: action.go-back
        
```
:::

### Restrict or filter the upload of media file types

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This example shows a form for a new employee, configured with a `media-field` component that allows the employee to upload their signed employment contract. File formats are restricted to DOC and PDF. The media picker opens and displays only PDF and DOC files for selection.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NX6I4Fub_rxtuUKR4UqHO-20250430-110158.gif" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-NX6I4Fub_rxtuUKR4UqHO-20250430-110158.gif" size="66" width="681" height="1377" position="center" caption="Filtered file types" alt="Filtered file types"}
:::
::::

:::CodeblockTabs
employee-contract.jigx

```yaml
title: Add new employee
type: jig.default
icon: person

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1740&q=80

children:
  - type: component.form
    instanceId: new-employee
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.number-field
          instanceId: employee-id
          options:
            label: employeeId
            isHidden: true
            initialValue: =($count(@ctx.datasources.employees-1.id) = 0 ? 1 :$count(@ctx.datasources.employees-1.id) + 1)
        - type: component.avatar-field
          instanceId: employee-photo
          options:
            label: Photo
        - type: component.section
          options:
            title: Personal informations
            children:
              - type: component.text-field
                instanceId: employee-first-name
                options:
                  label: First name
              - type: component.text-field
                instanceId: employee-surname
                options:
                  label: Surname
              - type: component.email-field
                instanceId: employee-email
                options:
                  label: Email
                  icon: email
              - type: component.number-field
                instanceId: employee-phone-number
                options:
                  label: Phone number
                  icon: phone
        - type: component.section
          options:
            title: Business informations
            children:
              - type: component.text-field
                instanceId: employee-position
                options:
                  label: Position
              - type: component.date-picker
                instanceId: employee-startWork
                options:
                  label: Date of starting work
              # Configure the media-field for uploading the contract.    
              - type: component.media-field
                instanceId: employee-contract
                options:
                  label: Contract
                  # Restrict the media files that can be uploaded to DOC & PDF.
                  # The picker will open and display all DOC & PDF files.
                  mediaType: 
                    - pdf
                    - doc
actions:
  - children:
      - type: action.submit-form
        options:
          formId: new-employee
          provider: DATA_PROVIDER_DYNAMIC
          title: Create Record
          entity: default/employees
          method: create
```
:::

### Upload images using REST&#x20;

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
&#x20;In this example the REST APIs POST operator is used to store images. A Jigx function with an `inputTransform` is used to capture the image metadata. Configuring the `conversion` property ensures that the images are uploaded in the correct format to the REST service.&#x20;

See the example in [Upload product images (POST)](<./../../Data Providers/REST/Create an app using REST APIs/Upload product images _POST_.md>) topic to understand how to upload files using the REST data provider.
:::

:::VerticalSplitItem
![Upload images using REST](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/9JpcY3lPb4m2WL0w-v4il_rest-image.PNG "Upload images using REST")
:::
::::

:::CodeblockTabs
add-customer-images.jigx

```yaml
title: Upload images
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/o1gobv6lj1l3076veyaff/cloud-7906280_1280.png?rlkey=c5ad2oknpw5fju9qjlb1c2d2o&raw=1
#Set the onFocus to clear all data from the jig and reset it for the next uplaod
onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.jig.components.newImage.state.data
    
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer
            value: =@ctx.jig.inputs.customer.companyName
  - type: component.form
    instanceId: newImage
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: description
          options:
            label: Add the product name
        - type: component.media-field
          instanceId: image
          options:
            label: image
            mediaType: image
            isMultiple: true
            maximumFileSize: =20 * 1024 * 1024

actions:
  - children:
      - type: action.execute-entities #Action to upload the images
        options:
          title: Upload images
          provider: DATA_PROVIDER_REST
          entity: customer-images
          method: create #Create the image record in the local SQLite table 
          function: rest-upload-customer-images #Create the image record in the REST service
          #Data configuration points to the collection of images with their metadata in the media-picker ensuring that the call to POST & create is executed multiple times for each image
            =@ctx.components.image.state.value.
            {
              "custId": @ctx.jig.inputs.customer.id,
              "createdBy": @ctx.user.email,
              "description": @ctx.jig.components.description.state.value,
              "createdDate": $now(),
              "image": $ 
            }
           onSuccess: 
             type: action.go-back  
```

rest-upload-images.jigx

```yaml
provider: DATA_PROVIDER_REST
# Creates data in the backend
method: POST 
# Use your REST service URL
url: https://jigx-training.azurewebsites.net/api/images 
# Direct the function call to use local execution,
# between the mobile device and the REST service. 
useLocalCall: true 
  
parameters:
  accessToken:
    location: header
    required: true
    type: string
# Use manage.jigx.com to define credentials for your solution
    value: service.oauth 

  custId:
    type: string
    location: body
    required: false
  createdBy:
    type: string
    location: body
    required: false
  description:
    type: string
    location: body
    required: false
  createdDate:
     type: string
     location: body
     required: false
     value: =$now()
  image:
    type: image
    location: body
    required: false
# Define the image metadata that must be created in the record,
# in the REST API.   
inputTransform: |
  {
    "custId": custId,
    "createdBy": createdBy,
    "description": description,
    "createdDate": createdDate,
    "image": image
  }
# Specifiying an outputTransform for the image_id ensure that the id,
# created by the REST API is automatically synced back to the 
# Jigx local datasource replacing the temp_id.    
outputTransform: |
  $.{
      "id": image_id
    }
# Convert the images to be uploaded to the REST service to base64,
# which the REST service expects to be able to store the image.  
conversions:
  - property: image
    from: local-uri
    to: base64
# Ensure images from iOS with a HEIC binary are viewable on Android,
# by converting the the image to JPG.   
    convertHeicToJpg: true
```
:::

### Use intialValue to show multiple images using REST

This example shows how multiple images can be loaded in the media-field using the `intialValue` property. Take note of the following configuration:

- The `initialValue` uses a datasource to return all the existing images. A local datasource ensures the images from the REST enpoint are stored locally on the device, for offline and performance reasons. The local datasource has a `queryParameter` restricting the images returned to be for the specific customer.
- To store images in the correct format a `conversion` is set on the REST POST function, converting the file from local-uri to base64. Added to this the `convertHeicToJpg` property is set to `true`, which allows the image to be viewable on iOS and Android.
- The media-field requires images to be in local-uri format, a conversion is set in the REST GET function, converting the file from base64 to local-uri.&#x20;
- When clicking on the `media-field` to add additional images the intial images are loaded in the field. Depending on the function used, for example POST,  if the images are not cleared or removed using the trash icon, the initial images will be uploaded as new images, creating duplicates. Using a PATCH or PUT function could avoid duplicates.

::Image[]{src="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-uWAWLJveF_UZewQnWNtgV-20240821-135959.PNG" signedSrc="https://archbee-doc-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-uWAWLJveF_UZewQnWNtgV-20240821-135959.PNG" size="68" width="2537" height="2508" position="center" caption="Load with intial images" alt="Load with intial images"}

:::CodeblockTabs
add-customer-images.jigx

```yaml
title: Upload images
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://www.dropbox.com/scl/fi/o1gobv6lj1l3076veyaff/cloud-7906280_1280.png?rlkey=c5ad2oknpw5fju9qjlb1c2d2o&raw=1

#Use a local datasource to return images & details,from the REST API.
datasources:
  all-products: 
    type: datasource.sqlite
    options:  
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: customer-images

      query: |
        SELECT 
          cim.id AS id,
          json_extract(cim.data, '$.createdDate') AS createdDate,
          json_extract(cim.data, '$.custId') AS custId,
          json_extract(cim.data, '$.createdBy') AS createdBy,
          json_extract(cim.data, '$.description') AS description,
          json_extract(cim.data, '$.image') AS image
        FROM 
          [customer-images] AS cim
        WHERE 
          json_extract(cim.data, '$.custId') = @custId
        ORDER BY 
          json_extract(cim.data, '$.createdDate') DESC
# Just return the images for the specific customer
      queryParameters:
        custId: =@ctx.jig.inputs.customer.id
                    
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Customer
            value: =@ctx.jig.inputs.customer.companyName
  - type: component.form
    instanceId: newImage
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: description
          options:
            label: Add the product name
        - type: component.media-field
          instanceId: image
          options:
# All images for the specificed customer will load when the jig opens.
# Add new images via the media-field.         
            initialValue: =@ctx.datasources.all-products.image
            label: image
            mediaType: image
            isMultiple: true
            maximumFileSize: =20 * 1024 * 1024

actions:
  - children:
      - type: action.execute-entities
        options:
          title: Upload images
          provider: DATA_PROVIDER_REST
          entity: customer-images
          method: create
          function: rest-upload-customer-images
          data: |
            =@ctx.components.image.state.value.
            {
              "custId": @ctx.jig.inputs.customer.id,
              "createdBy": @ctx.user.email,
              "description": @ctx.jig.components.description.state.value,
              "createdDate": $now(),
              "image": $ 
            }
           onSuccess: 
            type: action.go-back 
```

rest-get-images.jigx (function)

```yaml
provider: DATA_PROVIDER_REST
method: GET
url: https://jigx-training.azurewebsites.net/api/images?custId={custId}&includeImage=true
useLocalCall: true
forRowsWithValues: 
  custId: custId
  
parameters:
  accessToken:
    location: header
    required: true
    type: string
# Use manage.jigx.com to define credentials for your solution
    value: service.oauth 
  custId:
    type: string
    location: query
    required: true

outputTransform: |
  $.images.
    {
        "id": id,
        "custId": $$.inputs.custId,
        "createdDate": createdDate,
        "createdBy": createdBy,
        "description": description,
        "image": image
    }[]
#Convert the images returned from the REST service to local-uri,
# which the jig expects to be able to display the image.
conversions:
  - property: image
    from: base64
    to: local-uri
```

rest-upload-images.jigx (function)

```yaml
provider: DATA_PROVIDER_REST
# Creates data in the backend
method: POST 
# Use your REST service URL
url: https://jigx-training.azurewebsites.net/api/images 
# Direct the function call to use local execution,
# between the mobile device and the REST service. 
useLocalCall: true 
  
parameters:
  accessToken:
    location: header
    required: true
    type: string
# Use manage.jigx.com to define credentials for your solution
    value: service.oauth 

  custId:
    type: string
    location: body
    required: false
  createdBy:
    type: string
    location: body
    required: false
  description:
    type: string
    location: body
    required: false
  createdDate:
     type: string
     location: body
     required: false
     value: =$now()
  image:
    type: image
    location: body
    required: false
# Define the image metadata that must be created in the record,
# in the REST API.   
inputTransform: |
  {
    "custId": custId,
    "createdBy": createdBy,
    "description": description,
    "createdDate": createdDate,
    "image": image
  }
# Specifiying an outputTransform for the image_id ensure that the id,
# created by the REST API is automatically synced back to the 
# Jigx local datasource replacing the temp_id.    
outputTransform: |
  $.{
      "id": image_id
    }
# Convert the images to be uploaded to the REST service to base64,
# which the REST service expects to be able to store the image.  
conversions:
  - property: image
    from: local-uri
    to: base64
# Ensure images from iOS with a HEIC binary are viewable on Android,
# by converting the the image to JPG.   
    convertHeicToJpg: true
```
:::

### Convert files to buffer in SQL function

Jigx stores files as local files on the device and returns the file's URI as the default value. When saving these files to a data source, you must convert files from the local-uri to base64, data-uri, or buffer. The opposite is true when handling the files returned from the data source, you need to convert them from their saved state (base64, data-uri, or buffer) to a local-uri. In this example we upload a profile photo and convert from local-uri on the device to buffer for storage in SQL and then get the photo back from SQL and convert it from buffer to local-uri to display the photo as an avatar in a list. See [File handling]() for more information.

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gAVxsX1KLX2lFjBhNFGKA_cc-hiking.PNG" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/gAVxsX1KLX2lFjBhNFGKA_cc-hiking.PNG" size="80" width="2540" height="2500" position="center" caption="File conversion in SQL function" alt="File conversion in SQL function"}

:::CodeblockTabs
get-sql-function.jigx

```yaml
provider: DATA_PROVIDER_SQL
connection: hikers.azure
method: query
query: |
  SELECT
    id,
    name,
    contact,
    photo
  FROM
    hikers  
# add the conversion from buffer in SQL back to local-uri for display in the list jig
conversions:
  - property: photo
    from: buffer
    to: local-uri
```

update-sql-function

```yaml
provider: DATA_PROVIDER_SQL
connection: hikers.azure
method: query
query: |
   UPDATE hikers
    SET
      name = @name,
      contact = @contact,
      photo = @photo
    WHERE
      id = @hikersID
parameters:
  hikersID:
    type: string
    location: input
    required: true
  name:
    type: string
    location: input
    required: true
  contact:
    type: string
    location: input
    required: true
  photo:
    type: file
    location: input
    required: true
    encoding: binary
# add the conversion from local-uri which is what the media picker uses to buffer when the image is updated in SQL
conversions:
  - property: photo
    from: local-uri
    to: buffer
```

update-hiker.jigx

```yaml
title: Update details
type: jig.default
icon: climbing-mountain

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1682685797736-dabb341dc7de?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

onFocus: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL 
    entities:
      - entity: hikers 
# use the SQL function containing the conversion from buffer to local-uri to display the intialValue photo in the form media field       
        function: get-sql-function

datasources:
  friend-update: 
     type: datasource.sqlite
     options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: hikers
      query: |
        SELECT
          id,
          '$.name',
          '$.contact',
          '$.photo'
        FROM
          [hikers] 
        WHERE
         id = @friendId     
      queryParameters:
        friendId: =@ctx.jig.inputs.friendId
      
children:
  - type: component.form
    instanceId: hike_info
    options:
      isDiscardChangesAlertEnabled: false
      children:
        - type: component.text-field
          instanceId: id
          options:
            label: id
            initialValue: =@ctx.datasources.friend-update.id
            isHidden: true
        - type: component.text-field
          instanceId: name
          options:
            label: Hiker's name
            initialValue: =@ctx.datasources.friend-update.name
        - type: component.text-field
          instanceId: contact
          options:
            label: Mobile number
            initialValue: =@ctx.datasources.friend-update.contact
        - type: component.media-field
          instanceId: photo
          options:
  # control the size of the image to be stored in SQL
            imageCropping:
              height: 64
              width: 64
            label: Profile photo
            mediaType: image            
            initialValue: =@ctx.datasources.friend-update.photo

actions:
  - children:
      - type: action.execute-entity
        options:
          title: Update Record
          provider: DATA_PROVIDER_SQL
          entity: hikers
          method: functionCall
  # call the function containing the conversion from local-uri to buffer to update the iamge in SQL
          function: update-hikers
          functionParameters:
            hikersID: =@ctx.components.id.state.value
            name: =@ctx.components.name.state.value
            contact: =@ctx.components.contact.state.value
 # use the state.value to upload the image           
            photo: =@ctx.components.photo.state.value 
           onSuccess: 
             type: action.go-back
```

get-hiker-list.jigx

```yaml
title: My hiking friends
type: jig.list
icon: contact

header:
  type: component.jig-header
  options:
    height: medium
    children:
      type: component.image
      options:
        resizeMode: cover
        source:
          uri: https://images.unsplash.com/photo-1539635278303-d4002c07eae3?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

onFocus:
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL 
    entities:
      - entity: hikers 
 # use the SQL function containing the conversion from buffer to local-uri to display the avatar photo in the list     
        function: get-sql-function

onRefresh: 
  type: action.sync-entities
  options:
    provider: DATA_PROVIDER_SQL 
    entities:
      - entity: hikers   
        function: get-sql-function
     
datasources:
  friendsList: 
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_LOCAL
      entities:
        - entity: hikers
      query: |
        SELECT
          id,
          '$.name',
          '$.contact',
          '$.photo'
        FROM
        [hikers]    
data: =@ctx.datasources.friendsList
item:
  type: component.list-item
  options:
    title: =@ctx.current.item.name
    subtitle: =@ctx.current.item.contact
    leftElement: 
      element: avatar
      text: Profile
      uri: =@ctx.current.item.photo
    swipeable:
      left:
        - label: update
          icon: upload-brackets
          color: primary
          onPress: 
            type: action.go-to
            options:
              linkTo: update-details
              parameters:
                friendId: =@ctx.current.item.id
```
:::

## **See also**

- [Upload product images (POST)](<./../../Data Providers/REST/Create an app using REST APIs/Upload product images _POST_.md>)
- [File handling]()
- [State]()

