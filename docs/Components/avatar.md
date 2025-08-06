# avatar

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
Using the avatar component, display a profile photo, company logo, initials, or flags as unique visual identifiers.
:::

:::VerticalSplitItem
::Image[]{alt="Avatar preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jzGEzQeNzQZUvB-bk3iM__avatar.png" size="64" caption="Avatar preview" position="center" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jzGEzQeNzQZUvB-bk3iM__avatar.png" width="800" height="225" darkWidth="800" darkHeight="225"}
:::
::::

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

| **Core structure** |                                                                                                                                                                                                                                                                    |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `title`            | Add a title for the avatar, this is text displayed when the `uri` is empty. In the visual presentation, the `title` can be substituted by an image using the `uri` property. But the content of the text property has to be kept at least to the empty string: "") |

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>align</code></p>
    </td>
    <td selected="false" align="left">
      <p>By default the avatar is aligned <code>left</code> but can be changed to:</p>
      <ul>
      <li><code>center</code></li>
      <li><code>left</code></li>
      <li><code>right</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>size</code></p>
    </td>
    <td selected="false" align="left">
      <p>The size of the avatar can be set to:</p>
      <ul>
      <li><code>small</code></li>
      <li><code>regular</code></li>
      <li><code>large</code></li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>uri</code></p>
    </td>
    <td selected="false" align="left">
      <p>Source of the image to display as the avatar.</p>
    </td>
  </tr>
</table>

## Examples and code snippets

:::::ExpandableHeading
### Avatar as children of jig (profile picture)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Avatar - Profile picture](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TTYP3M3nKqHyamgxhEdjY_avatars-picturesiphone13blueportrait.png "Avatar - Profile picture")
:::

:::VerticalSplitItem
This example shows the avatar component in a jig. It can be used for employee headshots, company logos, or flags.

**Examples:**
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/static-data/avatar-as-children-of-jig/avatar-picture.jigx).
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/dynamic-data/avatar-as-children-of-jig/avatar-picture-dynamic.jigx).

**Datasources:**
See the full datasource code sample for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global.jigx).
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/dynamic-global.jigx).
:::
::::

:::CodeblockTabs
avatar-profile-picture (static)

```yaml
children:
  - type: component.avatar
    options:
      title:  ""
      uri: =@ctx.datasources.static-global.picture
      size: large
      align: center
  - type: component.avatar
    options:
      title:  ""
      uri: =@ctx.datasources.static-global.picture
      size: regular
      align: center
  - type: component.avatar
    options:
      title:  ""
      uri: =@ctx.datasources.static-global.picture
      size: small
      align: center
```

avatar-profile-picture (dynamic)

```yaml
children:
  - type: component.avatar
    options:
      title:  ""
      uri: =@ctx.datasources.dynamic-global.picture
      size: large
      align: center
  - type: component.avatar
    options:
      title:  ""
      uri: =@ctx.datasources.dynamic-global.picture
      size: regular
      align: center
  - type: component.avatar
    options:
      title:  ""
      uri: =@ctx.datasources.dynamic-global.picture
      size: small
      align: center
```

datasources (static)

```yaml
datasources:
  static-global:
    type: datasource.static
    options:
      data:
        - name: July Nelson
          picture: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          date_from: "2022-06-10T10:00:00Z"
          date_to: "2022-0610T10:30:00Z"
          email: grant@firs.com
          phone: 564332345
```

datasources (dynamic)

```yaml
datasources:
  dynamic-global:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/global
      query: |
        SELECT
          '$.name',
          '$.picture',
          '$.date-from',
          '$.date-to',
          '$.email',
          '$.phone'
        FROM [default/global]
```
:::
:::::

:::::ExpandableHeading
### Avatar as children of jig (initials)

::::VerticalSplit{layout="left"}
:::VerticalSplitItem
![Avatar with initials](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xzz8dVt34c8Y2tLAOQd-W_avatars-lettersiphone13blueportrait.png "Avatar with initials")
:::

:::VerticalSplitItem
As in the previous example, we use the avatar component for detail. In this case, we use the initials of the user or employee. It's useful if you don't have a picture of them.

**Examples:**
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/static-data/avatar-as-children-of-jig/avatar-initials.jigx).
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/dynamic-data/avatar-as-children-of-jig/avatar-initials-dynamic.jigx).

**Datasources:**
See the full datasource code sample for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global.jigx).
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/dynamic-global.jigx).
:::
::::

:::CodeblockTabs
avatar-initials (static)

```yaml
children:
  - type: component.avatar
    options:
      title:  =$substring($substringBefore(@ctx.datasources.static-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.static-global.name, " "), 0, 1)
      size: large
      align: center
  - type: component.avatar
    options:
      title:  =$substring($substringBefore(@ctx.datasources.static-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.static-global.name, " "), 0, 1)
      size: regular
      align: center
  - type: component.avatar
    options:
      title:  =$substring($substringBefore(@ctx.datasources.static-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.static-global.name, " "), 0, 1)
      size: small
      align: center
```

avatar-initials (dynamic)

```yaml
children:
  - type: component.avatar
    options:
      title:  =$substring($substringBefore(@ctx.datasources.dynamic-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.dynamic-global.name, " "), 0, 1)
      size: large
      align: center
  - type: component.avatar
    options:
      title:  =$substring($substringBefore(@ctx.datasources.dynamic-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.dynamic-global.name, " "), 0, 1)
      size: regular
      align: center
  - type: component.avatar
    options:
      title:  =$substring($substringBefore(@ctx.datasources.dynamic-global.name, " "), 0, 1) & $substring($substringAfter(@ctx.datasources.dynamic-global.name, " "), 0, 1)
      size: small
      align: center
```

datasources (static)

```yaml
datasources:
  static-global:
    type: datasource.static
    options:
      data:
        - name: July Nelson
          picture: https://images.unsplash.com/photo-1546961329-78bef0414d7c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=774&q=80
          date_from: "2022-06-10T10:00:00Z"
          date_to: "2022-06-10T10:30:00Z"
          email: grant@first.com
          phone: 564332345
```

datasources (dynamic)

```yaml
datasources:
  dynamic-global:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/global
      query: |
        SELECT
          '$.name',
          '$.picture',
          '$.date-from',
          '$.date-to',
          '$.email',
          '$.phone'
        FROM [default/global]
```
:::
:::::

