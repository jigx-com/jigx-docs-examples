# Custom components (Alpha)

## Custom components (Alpha)

### Custom components (Alpha)

{% hint style="danger" %}
This feature is currently in its **Alpha** stage of development.
{% endhint %}

* As an early version, it may not include all planned functionalities and is subject to significant changes based on ongoing development and user feedback.
* In this phase, the feature may contain bugs or behave unpredictably.
* Jigx recommends using standard, fully supported components until this feature has been fully tested and refined.
* We encourage you to provide feedback and report any issues to help us improve and refine the feature for future releases.&#x20;

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

1. In Jigx Builder in the components folder, create a new jigx file, e.g., custom-button.jigx.
2. Select the `type: component.default`. All custom components require this type.
3. Under the `children:` property, use IntelliSence (Ctrl+space) to see the list of available components. Select the components, e.g., `type: component.button`.
4. Under the `options:` properties, create a space and use **ctrl+space** to open the IntelliSense popup\*\*.\*\*
5. You can select the styling properties from the list shown.
6. Configure the other properties provided in the code snippet.
7. Open the jig where you want to use the custom component and reference `component.custom-component`. Use the `componentId` property to reference the name of the custom component file, e.g., `componentId: custom-button`.
8. Test the jig on a mobile device to ensure the button is rendering correctly.

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

{% tabs %}
{% tab title="Correct YAML" %}
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
{% endtab %}

{% tab title="Incorrect YAML" %}
```yaml
# Incorrect YAML snippet for using the height property in the image component,
# when used in a custom component.
- type: component.image
          options:
            height: 196
            source:
              uri: https://images
```
{% endtab %}
{% endtabs %}
