# text-field

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
The text field is a versatile component, allowing many variations and configurations. It allows users to enter letters, numbers, and special signs on a single or multiple lines.
:::

:::VerticalSplitItem
::Image[]{alt="Text Field Preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zbpFBEDL54rUVnRZH8gFa_text.png" size="76" caption="Text Field Preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/zbpFBEDL54rUVnRZH8gFa_text.png"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------ |
| `instanceId`       | Provide a unique Id for the component that can be referenced elsewhere.              |
| `label`            | Give the field a label. Label is displayed as placeholder when no value is provided. |

| **Other options**                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `autoCapatilize`                  | This property automatically capatilzes certain parts of the text input depending on the selection made. The keyboard caps lock is automatically set depending on the selection made. This property is not supported by certian keyboard types such as name-phone-pad.&#xA;The following options are available:&#xA;`characters` - capatilizes the all characters.&#xA;`sentences` - capatilizes all words in a sentence.&#xA;`none` - nothing is automatically capatalized.&#xA;`words` - capatilizes all words.                                 |
| `color`                           | There is a list of colors available. The color is used in combination with the condition `when`. See [Jigx color palette](#) for the available color options.                                                                                                                                                                                                                                                                                                                                                                                    |
| `errortext`                       | Add text, string, or expressions to show text under the text-field indicating an error/invalid value in the field. Text is shown in `isNegative` (red) styling with a red exclamation icon on the right.                                                                                                                                                                                                                                                                                                                                         |
| `format`                          | Text format of the value entered. For example, percentage or currency. Formatting only displays in the app when the input field is set to disabled (read-only).                                                                                                                                                                                                                                                                                                                                                                                  |
| `helperText`                      | Add text, string, or expressions to guide users by showing text under the number-field. Helper text is displayed only when there is no errorText.                                                                                                                                                                                                                                                                                                                                                                                                |
| `KeyboardType`                    | Determines which keyboard to open. There is a list to select from, certain keyboard selections require a specific device or virtual keyboard.                                                                                                                                                                                                                                                                                                                                                                                                    |
| `icon`                            | There is a list of icons available, see [Jigx icons](#) for more information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `initialValue`                    | The `initialValue` is the value that will be displayed in the text-field when the form is initially loaded. You can use this property to preset the field with default text so that you do not have to manually select it.  Useful when creating an edit or update form. Using the `reset-state` action with `initialValues` does not clear the field, it resets the field back to it's `initialValue`.                                                                                                                                          |
| `isAutocorrected`                 | Set to `false`, disables auto-correct. The default value is `true`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `isAutoFocused`                   | If `true` the text-field will get focus immediately after the form is displayed and the keyboard will be opened automatically.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `isHidden`                        | If `true` the text-field will be hidden on the form. If set to `false` the field will be shown.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `isIgnored`                       | When `true`, the field will be ignored when submitting the form and the content will not be stored.                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `isMultiline`                     | Set to `true` allows for multiple line text input. The default value is `false` setting the field to single line.                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `isOptionalLabelHidden`           | If the field is optional you can turn off the "(optional)" label by setting this field to `true`. This property works in combination with `isRequired: false`.                                                                                                                                                                                                                                                                                                                                                                                   |
| `isRequired`                      | Set to `true` when the field is required. Useful when you use it in form submission as the submit button remains disabled until the text-field has an input. Set to `false` the field is optional and will have (optional) in the label.                                                                                                                                                                                                                                                                                                         |
| `isReturnKeyEnabledAutomatically` | When set to `true`, the keyboard disables the return/done key when there is no text and automatically enables it when there is a text. The default value is `false`.                                                                                                                                                                                                                                                                                                                                                                             |
| `isSensitive`                     | If set to `true`, the input obscures the text entered so that sensitive text stays secure. For example, bank card account details, passwords or salary details.                                                                                                                                                                                                                                                                                                                                                                                  |
| `istextClearedOnFocus`            | When set to `true`, the text-field is automatically cleared when editing begins.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `minLength`                       | Specifies the minimum number of characters allowed in the field.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `maxLength`                       | Specifies the maximum number of characters allowed in the field.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| `nextProperty`                    | Name of the property you want to focus next in the form when you use return/next on a keyboard.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `returnKeyType`                   | Determines the label of the return key on the keyboard, for example, `done`, `search`, `join` or `next`. On Android you can use `returnKeyLabel`.                                                                                                                                                                                                                                                                                                                                                                                                |
| `style`                           | The following property settings are available:&#xA;- `flex` - Flex property if rendered inside row.&#xA;- `isBusy` - Displays spinner on right side of field. It removes any  configured icon.&#xA;- `isDisabled` - disables the number-field preventing any input text.&#xA;- `isPositive` - a green icon displays on the right of the number-field.&#xA;More than one can be true. It will be evaluated based on priority.                                                                                                                     |
| `textArea`                        | Sets the height of the text area. This property should be used in conjunction with `isMultiline`. The following property settings are available:&#xA;- `dynamic` allows the height to change based on the text content. &#xA;- `small` &#xA;- `medium`  &#xA;- `large` set the height to a relative size with a dynamic edit size.&#xA;The default is undefined, which uses a static height.                                                                                                                                                     |
| `textContentType`                 | If you have setup your phone with your details these can be used as autofill hints to select for populating the text-field.&#xA;For iOS 11+ you can set `textContentType` to `username` or `password` to enable autofill of login details from the device keychain. For iOS 12+ `newPassword` can be used to indicate a new password input the user may want to save in the keychain, and `oneTimeCode` can be used to indicate that a field can be autofilled by a code arriving in an SMS. To disable autofill, set `textContentType` to none. |
| `Value`                           | The value to show in the text-field when the form initially loads. This can be combined with the `isDisable` style to preset the value that cannot be edited on the form.                                                                                                                                                                                                                                                                                                                                                                        |

| **Actions** |                                                                                                                                            |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `onChange`  | The action is triggered when the content in the text-field is changed. Use IntelliSense (ctrl+space) to see the list of available actions. |

| **State Configuration**  | **Key**              | **Notes**                                                       |
| ------------------------ | -------------------- | --------------------------------------------------------------- |
| `=@ctx.component.state.` | value                | State is the variable of the component.                         |
| `=@ctx.solution.state.`  | activeItemId&#xA;now | Global state variable that can be used throughout the solution. |

## Considerations

- When using the `contentType: phone`, ensure the phone number entered contains no spaces; this allows you to click on the field to initiate a call from your device.

## Examples and code snippets

::::ExpandableHeading
### Text fields on a Form

::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2QrorTKAQD9Zq_WBOyoYt_cc-text-field.png" size="80" position="center" caption="Form with text-fields" alt="Form with text-fields" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2QrorTKAQD9Zq_WBOyoYt_cc-text-field.png"}

In this example five text-fields are used, namely:

1. The *name* text-field uses `minLength` and `maxLength` and `helpText` properties.
2. The *Zip/Postal code* text-field uses the `isRequired` property set to `false` making the field optional. The `autoCapitalize` property is set to `character` to ensure the keyboard caps lock is on for all characters typed in the field.
3. The *claim details* text field uses the `isMultiline` set to `true` and `textArea` set to `medium` allowing for a full description to be input.
4. The OTP text-field property use the `errorText` and `isSensitive` properties ensuring the OTP number is obscured.
5. The submission text-field is set as `style: IsDisabled: true` with a `color` and `icon` to be displayed.

**Examples:**

See the full example using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/text-field/static-data/text-field.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/text-field/dynamic-data/text-field-dynamic.jigx).

:::CodeblockTabs
text-field (static)

```yaml
title: text-field
type: jig.default

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://images.unsplash.com/photo-1592431913823-7af6b323da9b?q=80&w=2340&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D

children:
  - type: component.form
    instanceId: newApplicant
    options:
      children:
        - type: component.text-field
          instanceId: name
          options:
            minLength: 5
            maxLength: 30
            helperText: Provide your name and surname
            label: Full Name
        - type: component.text-field
          instanceId: address
          options:
            isRequired: false
            autoCapitalize: characters
            label: Zip/Postal code   
        - type: component.text-field
          instanceId: claimDetails
          options:
            isMultiline: true
            textArea: medium
            label: Provide details of the claim
        - type: component.text-field
          instanceId: claimOTP
          options:
            errorText: That is not a valid OTP number
            isSensitive: true
            label: Provide the claim One-Time-Password
        - type: component.text-field
          instanceId: claimStatus
          options:
            color:
              - when: true
                color: color6
            style:
              isDisabled: true
            icon: check-2-alternate
            label: Submission
            value: Ready for submission
```

text-field (dynamic)

```yaml
children:
  - type: component.form
    instanceId: text-form
    options:
      children: 
        - type: component.text-field
          instanceId: firstname
          options:
            label: Name
            helperText: =@ctx.datasources.field-values.text
```

datasources (dynamic)

```yaml
datasources:
  field-values:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/value
      query: |
        SELECT
          '$.id',
          '$.number',
          '$.text',
          '$.email',
          '$.category'
        FROM [default/value] WHERE '$.category' = "field-category"
```
:::
::::

### Use textContentTypes to autofill text-fields

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Setting certain information in your device, for example in *Settings* on iPhone, will allow you to be able to autofill forms quickly and accurately. Then use the `contentType` property in the `text-field` on a Jigx form to specific the type, such as name, address, credit-card and more. If the information is available on the device, tapping on the field will provide an autofill hint that can be selected and the field will autofill with the details.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-IBEOlcBj16-e73Qgk9MdA-20240822-073444.gif" size="90" position="center" caption="Autofill text fields" alt="Autofill text fields" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-IBEOlcBj16-e73Qgk9MdA-20240822-073444.gif"}
:::
::::

:::CodeblockTabs
content-type.jigx

```yaml
title: Content types
type: jig.default
icon: content-browser-edit

header:
  type: component.jig-header
  options:
    height: small
    children:
      type: component.image
      options:
        source:
          uri: https://builder.jigx.com/assets/images/captureinfo.jpg

actions:
  - children:
      - type: action.action-list
        options:
          title: Create Contact
          isSequential: true
          actions:
            - type: action.execute-entity
              options:
                provider: DATA_PROVIDER_DYNAMIC
                entity: default/contacts
                method: create
                data:
                  name: =@ctx.components.name.state.value
                  surname: =@ctx.components.surname.state.value
                  phone: =@ctx.components.phone.state.value
                  address:  =@ctx.components.phone.state.value
                  onSuccess:
                  title: Your contact details were successfully created.    
            - type: action.go-back

children: 
  - type: component.form
    instanceId: Info
    options:
    isDiscardChangesAlertEnabled: false
      children:
        - type: component.field-row
          options:
            children:
              - type: component.text-field
                instanceId: name
                options:
# Provide the autofill hint for first name using textContentType                 
                  textContentType: givenName
                  label: First Name
              - type: component.text-field
                instanceId: surname
                options:
# Provide the autofill hint for surname using textContentType                
                  textContentType: familyName
                  label: Last Name 
        - type: component.text-field
          instanceId: phone
          options:
# Provide the autofill hint for phone numbers using textContentType          
            textContentType: telephoneNumber
            label: Contact us
            icon: phone
        - type: component.text-field
          instanceId: address
          options:
# Provide the autofill hint for street address using textContentType          
            textContentType: fullStreetAddress
            label: Address
            icon: maps-pin-1         
```
:::

## See also

- [State](#)

