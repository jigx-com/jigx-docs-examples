# avatar

{% columns %}
{% column %}
Using the avatar component, display a profile photo, company logo, initials, or flags as unique visual identifiers.
{% endcolumn %}

{% column %}
Image\[]{alt="Avatar preview" src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/jzGEzQeNzQZUvB-bk3iM\_\_avatar.png
{% endcolumn %}
{% endcolumns %}

### Configuration options

Some properties are common to all components, see [Common component properties](avatar.md) for a list and their configuration options.

<table data-header-hidden><thead><tr><th width="145.1015625">Core structure</th><th></th></tr></thead><tbody><tr><td><code>title</code></td><td>Add a title for the avatar, this is text displayed when the <code>uri</code> is empty. In the visual presentation, the <code>title</code> can be substituted by an image using the <code>uri</code> property. But the content of the text property has to be kept at least to the empty string: "")</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th width="146.9296875">Other options</th><th></th></tr></thead><tbody><tr><td><code>align</code></td><td><p>By default the avatar is aligned <code>left</code> but can be changed to:</p><ul><li><code>center</code></li><li><code>left</code></li><li><code>right</code></li></ul></td></tr><tr><td><code>size</code></td><td><p>The size of the avatar can be set to:</p><ul><li><code>small</code></li><li><code>regular</code></li><li><code>large</code></li></ul></td></tr><tr><td><code>uri</code></td><td>Source of the image to display as the avatar.</td></tr></tbody></table>

### Examples and code snippets

#### Avatar as children of jig (profile picture)

{% columns %}
{% column %}
![Avatar - Profile picture](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/TTYP3M3nKqHyamgxhEdjY_avatars-picturesiphone13blueportrait.png)
{% endcolumn %}

{% column %}
This example shows the avatar component in a jig. It can be used for employee headshots, company logos, or flags.

**Examples:** \
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/static-data/avatar-as-children-of-jig/avatar-picture.jigx). \
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/dynamic-data/avatar-as-children-of-jig/avatar-picture-dynamic.jigx).

**Datasources:** \
See the full datasource code sample for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global.jigx). \
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/dynamic-global.jigx).&#x20;
{% endcolumn %}
{% endcolumns %}

:::CodeblockTabs&#x20;

{% tabs %}
{% tab title="avatar-profile-picture (static)" %}
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
{% endtab %}

{% tab title=" avatar-profile-picture (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (static)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}

#### Avatar as children of jig (initials)

{% columns %}
{% column %}
&#x20;![Avatar with initials](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/xzz8dVt34c8Y2tLAOQd-W_avatars-lettersiphone13blueportrait.png)&#x20;
{% endcolumn %}

{% column %}
As in the previous example, we use the avatar component for detail. In this case, we use the initials of the user or employee. It's useful if you don't have a picture of them.

**Examples:** \
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/static-data/avatar-as-children-of-jig/avatar-initials.jigx). \
See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/avatar/dynamic-data/avatar-as-children-of-jig/avatar-initials-dynamic.jigx).

**Datasources:** \
See the full datasource code sample for static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/static-global.jigx). \
See the full datasource code sample for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/examples/dynamic-global.jigx)
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="avatar-initials (static)" %}
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
{% endtab %}

{% tab title="avatar-initials (dynamic)" %}
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
{% endtab %}

{% tab title="datasources (static)" %}
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
{% endtab %}

{% tab title="datasources (dynamic)" %}
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
{% endtab %}
{% endtabs %}
