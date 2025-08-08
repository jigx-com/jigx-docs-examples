# Date & Time

Date and time expressions use the :Link[JSONata Date/Time functions]{href="https://docs.jsonata.org/date-time-functions" newTab="true" hasDisabledNofollow="false"} to return various formats of date/time, date, or time. These expressions are used to get the current timestamp in ISO 8601 formatted string, use an expression over the timestamp to convert the timestamp into a specific format.

## Configuration

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="313">
  <tr>
    <td selected="false" align="left">
      <p><strong>Result</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Expression</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current timestamp as ISO 8601</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$now()</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current datetime in milliseconds</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$toMillis($now())</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current date [M]/[D]/[Y]</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[M]/[D]/[Y]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current date [M01]/[D01]/[Y0001]</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current datetime '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]'</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current date [MI]/[DI]/[YI]</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[MI]/[DI]/[YI]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current date [D1o] [MNn] [Y]</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[D1o] [MNn] [Y]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current day</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[FNn]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current time</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[H01]:[m01]:[s01]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current time am/pm</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[h#1]:[m01][P]')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Current time '[H01]:[m01]:[s01] [z]', '-0500'</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis($toMillis($now()), '[H01]:[m01]:[s01] [z]', '-0500')</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Convert UTC to milliseconds</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$toMillis()</code></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p>Convert millisecond to UTC</p>
    </td>
    <td selected="false" align="left">
      <p><code>=$fromMillis()</code></p>
    </td>
  </tr>
</table>

## Consideration

- When using `=$now()` on a component level,  the date/time is not refreshed when navigating out and into the jig. To cater to this scenario, add an `onFocus` with a `set-state` action to the jig.

:::CodeblockTabs
component

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Order Date
            value: =@ctx.solution.state.now
```

onFocus

```yaml
onFocus: 
  type: action.set-state
  options:
    state: =@ctx.solution.state.now
    value: =$now()
```
:::

:::hint{type="warning"}
Be careful when using complex expressions, such as expressions that iterate one datasource across another, as your solution performance could become slower. To avoid this, try to use the datasource queries to get the desired result rather than an expression.
:::

## Examples and code snippets

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rLyfpAJd6UWubCCOtnOx8_img6600iphone13blueportrait.png" size="72" position="center" caption="Date & time expressions" alt="Date & time expressions" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/rLyfpAJd6UWubCCOtnOx8_img6600iphone13blueportrait.png" width="800" height="1493" darkWidth="800" darkHeight="1493"}
:::

:::VerticalSplitItem
This example uses a component.enitity to show the results of various date/time functions

See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/guide-expressions/static-data/expression.jigx).
:::
::::

:::CodeblockTabs
expression.jigx

```yaml
children:
  - type: component.entity
    options:
      children:
        - type: component.entity-field
          options:
            label: Current timestamp as ISO 8601
            value: =$now()
        - type: component.entity-field
          options:
            label: Current datetime in milliseconds
            value: =$toMillis($now())
        - type: component.entity-field
          options:
            label: Current date [M]/[D]/[Y]
            value: =$fromMillis($toMillis($now()), '[M]/[D]/[Y]')
        - type: component.entity-field
          options:
            label: Current date [M01]/[D01]/[Y0001]
            value: =$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001]')
        - type: component.entity-field
          options:
            label: Current datetime '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]'
            value: =$fromMillis($toMillis($now()), '[M01]/[D01]/[Y0001] [H01]:[m01]:[s01]')
        - type: component.entity-field
          options:
            label: Current date [MI]/[DI]/[YI]
            value: =$fromMillis($toMillis($now()), '[MI]/[DI]/[YI]')
        - type: component.entity-field
          options:
            label: Current date [D1o] [MNn] [Y]
            value: =$fromMillis($toMillis($now()), '[D1o] [MNn] [Y]')
        - type: component.entity-field
          options:
            label: Current day
            value: =$fromMillis($toMillis($now()), '[FNn]')
        - type: component.entity-field
          options:
            label: Current time
            value: =$fromMillis($toMillis($now()), '[H01]:[m01]:[s01]')
        - type: component.entity-field
          options:
            label: Current time am/pm
            value: =$fromMillis($toMillis($now()), '[h#1]:[m01][P]')
        - type: component.entity-field
          options:
            label: Current time '[H01]:[m01]:[s01] [z]', '-0500'
            value: =$fromMillis($toMillis($now()), '[H01]:[m01]:[s01] [z]', '-0500')
```
:::

