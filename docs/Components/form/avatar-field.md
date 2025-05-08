---
title: avatar-field
slug: AuZa-avatar-field
description: Learn how to effectively use the avatar field component in your forms to upload images. This document highlights its configuration options, such as instance ID, label, icon, color, and maximum file size. Discover how to save images using dynamic or SQL da
createdAt: Mon Jul 04 2022 09:02:33 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Aug 23 2024 13:04:24 GMT+0000 (Coordinated Universal Time)
---

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This component allows you to upload an avatar image. You can choose a picture from your device or use your camera to capture one.
:::

:::VerticalSplitItem
::Image[]{alt="Avatar Field Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/-_UiZpMFDyAN1buxUcz3m_avatar-field.png" size="72" caption="Avatar Field Preview" position="center" }
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                            |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `instanceId`       | The unique identifier for the avatar-field.        |
| `label`            | Provide a label/name for the avatar. 'Label' is displayed as a placeholder when no value is specified. **Note** the label is displayed at the top of the popup screen where you select images. |

| **Other options**       |    |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `color`                 | Sets the color of the avatar-field based on conditions by using the when property. First evaluated to true will be used. Choose a color from the provided color palette. Default color is grey if the property is not specified in the YAML. See the list of available colors in [Jigx color palette]().                                 |
| `errorText`             | Add text, string, or expressions to show text under the avatar-field indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling.                                                                                                                                                                        |
| `helperText`            | Add text, string, or expressions to guide users by showing text under the avatar-field. Helper text is displayed only when there is no errorText.                                                                                                                                                                                        |
| `imageQuality`          | Image quality after compression (from 0 to 100, where 100 is the best quality). On iOS, values larger than 80 don't produce a noticeable quality increase in most images, while a value of 80 will reduce the file size by about half or less compared to a value of 100. Default: 100 (Android)/ 80 (iOS).                              |
| `icon`                  | Add an icon to the title. A list of icons is available. See [Jigx icons]() for more information.     |
| `imageCropping`         | You can set the following with `imageCropping` :&#xA;`isEnabled` - allows you to crop an image if set to `true`. &#xA;`isFreeStyleCropEnabled` - when set to `true` it supports custom cropping to change the size or aspect ratio of an image.&#xA;`height` - maximum allowed is 5000px&#xA;`width`- maximum allowed is 5000px          |
| `initialValue`          | Initial value of the relevant field. You can use this to preset value, so user doesn't need to add anything and use this "default". Using the `reset-state` action with `initialValues` does not clear the field, it resets the field back to it's `initialValue`.                                                                       |
| `isAutoFocused`         | If `true` it will get focus immediately after it is displayed.   |
| `isHidden`              | If `true` the avatar-field will be hidden on the form. If set to `false` the field will be shown.       |
| `isIgnored`             | When `true`, the field will be ignored when submitting the form and the content will not be stored.    |
| `isOptionalLabelHidden` | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. **Note** the (optional) text in the label is displayed at the top of the popup screen where you select images. This property works in combination with `isRequired: false`.                                                            |
| `isRequired`            | Set to `true` when the field is required. Useful when you use it in form submission. When set to `false` the (optional) text in the label is displayed at the top of the popup screen where you select images.     |
| `maximumFileSize`       | Maximum file size in bytes. Set to 'none' to disable size check. Default value is `=6 * 1024 * 1024` 6MB.    |
| `nextProperty`          | Name of the property you want to focus next in the form when you use return/next on a keyboard.     |
| `style`                 | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isBusy` - Displays a spinner. &#xA;- `isDisabled` - disables the avatar-field preventing the image selection popup from displaying.&#xA;- `isPositive`&#xA;More than one can be true. It will be evaluated based on priority. |
| `value`                 | The value to show for the field. Text field is a controlled component, which means the internal value will be forced to match this value prop if provided. In most cases, you don't need to use this.    |

| **Actions**|   |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `onChange`  | The action is triggered when the content in the avatar-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions.  |

| ### State Configuration  | **Key**              | **Notes**                                                         |
| ------------------------ | -------------------- | ----------------------------------------------------------------- |
| `=@ctx.component.state.` | value                | - State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | * Global state variable that can be used throughout the solution. |

## Considerations

- The `avatar-field` can only be used in a [jig.default](<./../../Jig Types/jig_default.md>) inside of a [form](./../form.md) component.
- Only Dynamic Data or SQL data can be used to ensure that the image can be saved.

## Examples and code snippets 

:::::ExpandableHeading
### Avatar field example

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Avatar ](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zzGERUU6kEdLrZ3bKcKFy_q75ewfno5lmiohkj-lv9avatarfieldiphone13blueportrait.png "Avatar ")
:::

:::VerticalSplitItem
This component uploads pictures for avatars.  After clicking on the plus next to the avatar, a menu will appear to choose whether to upload an existing image from your device or use the camera to take a new image. After loading and cropping the image, press the Upload picture button at the bottom to call the action to save the image.

**Examples:**

See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar-field/dynamic-data/avatar-field-example/avatar-field-example.jigx)
:::
::::

:::CodeblockTabs
avatar (dynamic)

```yaml
children:
  - type: component.form
    options:
      children:
        - type: component.avatar-field
          instanceId: avatar-field
          options:
            label: Upload avatar
            color:
              - when: true
                color: color2
            style:
              flex: 1
            imageCropping:
              width: 120
              height: 120
            isHidden: false
            isIgnored: false
```
:::
:::::

## See also

- [State]()

