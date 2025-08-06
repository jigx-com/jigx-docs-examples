# actions (buttons)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
This widget allows you to add primary and/or secondary actions (buttons) to a widget. This is a quick way for users to perform actions without needing to access a jig through the widget first.

- Any of the actions that are available in the [Actions](./../Actions.md) section can be configured on the widget.
- This widget can be configured in a [group](<./Content widget components/group.md>) widget, which allows you to group the actions with other widget types.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bXQzrMgA9C2WU-VcYpOYU_wd-actions.png" size="58" position="center" caption="Action widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/bXQzrMgA9C2WU-VcYpOYU_wd-actions.png" width="800" height="840" darkWidth="800" darkHeight="840"}
:::
::::

## Configuration options

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="138">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onPress</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure the action to be executed when the action button is pressed.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>title</code></p>
    </td>
    <td selected="false" align="left">
      <p>Display the text content for the title.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="137">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>footer</code></p>
    </td>
    <td selected="false" align="left">
      <p>Add text to the footer of the widget.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>footerAlign</code></p>
    </td>
    <td selected="false" align="left">
      <p>Align the footer text to <code>left</code>, <code>right</code>, <code>center</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>placeholders</code></p>
    </td>
    <td selected="false" align="left">
      <p>Specify a placeholder text to display if there is no data, for example - <code>title: No data to display</code>.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>primary</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure a <code>title</code> and onPress properties for a primary action button.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>secondary</code></p>
    </td>
    <td selected="false" align="left">
      <p>Configure a <code>title</code> and <code>onPress</code> properties for a secondary action button.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Example of actions widget

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VtuoNb4XzobXvjv_YNiP9_actionsiphone13blueportrait.png" size="80" position="center" caption="Actions widget" alt="Actions widget" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VtuoNb4XzobXvjv_YNiP9_actionsiphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
Here is an example of the actions button on the widget level. When the primary button is pressed, an avatar is shown, and when the secondary button (white with blue text) is pressed, the color palette is shown.

**Examples**:
See the complete example in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/widgets/action/actions.jigx).
:::
::::

:::CodeblockTabs
actions-widget

```yaml
widgets:
  actions-2x2:
    type: widget.actions
    options:
      footer: Show more
      footerAlign: center
      primary:
        title: Avatar info
        onPress:
          type: action.go-to
          options:
            linkTo: avatar-field-example
      secondary:
        title: Color palette
        onPress:
          type: action.go-to
          options:
            linkTo: color-palete
```

grid-item

```yaml
# Grid-item for the jig.
children:
  - type: component.grid-item
    options:
      size: "2x2"
      children: 
        type: component.jig-widget
        options:
          jigId: actions-widget
          widgetId: actions-2x2
```
:::
:::::

