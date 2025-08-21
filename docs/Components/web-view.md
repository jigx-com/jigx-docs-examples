# web-view

This component displays a webpage from a specified URL, content from a datasource, or custom HTML.

{% hint style="info" %}
&#x20;You can also use the [jig.document](<../Jig Types/jig_document.md>) type to display web pages in full-screen mode or pass messages from your HTML content via JavaScript to the Jigx App.
{% endhint %}

## Configuration options

Some properties are common to all components, see [Common component properties](web-view.md) for a list and their configuration options.

<table><thead><tr><th width="278.1953125">Core structure</th><th></th></tr></thead><tbody><tr><td><code>uri</code></td><td>The source to be displayed in the web-view, for example, a URL.</td></tr></tbody></table>

<table><thead><tr><th width="281.4453125">Other options</th><th></th></tr></thead><tbody><tr><td><code>content</code></td><td>HTML to render in the web-view.</td></tr><tr><td><code>height</code></td><td>The height of the web-view.</td></tr><tr><td><code>isEditable</code></td><td>A very basic implementation, if set to <code>true</code>, the web-view <code>content</code> becomes editable. This works only with <code>content</code>, not with a <code>uri</code>. The <code>isEditable</code> property is only available when using the web-view in a .</td></tr><tr><td><code>isTrackingTransparencyRequired</code></td><td>If set to <code>true</code> tracking transparency permission modal is shown before opening the URL. The default setting is <code>true</code>.</td></tr></tbody></table>

## Consideration

* The `component.web-view` can be used in [jig.fullscreen](<../Jig Types/jig_fullscreen.md>), if the content needs to fill the screen.

## Examples and code snippets

### Web-view example (URL)

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VeM3NrBpP0oAm20xE\_SLn\_img9582iphone13blueportrait.png" size="80" position="center" caption="Web-view with URL " alt="Web-view with URL " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VeM3NrBpP0oAm20xE\_SLn\_img9582iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
{% endcolumn %}

{% column %}
In this example, we open a target URL in the web-view component.

If the target URL is tracking data (e.g., cookies etc.), you are required by Apple to ask for user consent using the `isTrackingTransparencyRequired` option. It will ask for user consent the first time any web view in your solution tries to open a target URL.

**Examples**: See the full example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/web-view/static-data/web-view-example/web-view-example.jigx). See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/web-view/dynamic-data/web-view-example-dynamic/web-view-example-dynamic.jigx).

**Datasource**: See the full datasource for static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/web-view.jigx). See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/web-view-dynamic.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="web-view (static)" %}
```yaml
type: jig.default
title: Web view

children:
  - type: component.web-view
    options:
      uri: =@ctx.datasources.web-view.url
      isTrackingTransparencyRequired: true
```
{% endtab %}

{% tab title="web-view (dynamic)" %}
```yaml
type: jig.default
title: Web view
isScrollable: false

children:
  - type: component.web-view
    options:
      uri: =@ctx.datasources.web-view-dynamic.uri
      isTrackingTransparencyRequired: true
      height: 1000
```
{% endtab %}

{% tab title="datasources (static)" %}
```yaml
datasources:
  web-view:
    type: datasource.static
    options:
      data:
        - url: https://www.jigx.com
```
{% endtab %}

{% tab title="datasources (dynamic)" %}
```yaml
datasources:
  web-view-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/links
      query: |
        SELECT
          '$.uri',
          '$.category'
        FROM [default/links] 
        WHERE '$.category' = "web-view"
```
{% endtab %}
{% endtabs %}

### Web-view example (HTML Content)

{% columns %}
{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/iUGy63w8idJuWWfsn9RKv\_img9581iphone13blueportrait.png" size="80" position="center" caption="Web-view with HTML content" alt="Web-view with HTML content" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/iUGy63w8idJuWWfsn9RKv\_img9581iphone13blueportrait.png" width="800" height="1494" darkWidth="800" darkHeight="1494"}
{% endcolumn %}

{% column %}
In this example, we are passing raw HTML content to the web-view component. This can either be inline content (see example below) or content from a datasource. If your HTML content does not render as expected (e.g. font too small etc.) embed the meta HTML tag used in the example below in your HTML content.
{% endcolumn %}
{% endcolumns %}

{% code title="web-view-raw" %}
```yaml
title: Web-View
type: jig.default

children:
  - type: component.web-view
    options:
      content: |
        <html>
          <head>
            <meta name="viewport" content="width=device-width, initial-scale=1">
          </head>
          <body>
            Hello World
          </body>
        </html>
```
{% endcode %}

### Editable web-view content (Fullscreen)

{% columns %}
{% column %}
In this example, the web-view component is used to make notes on a job. It is configured in a `jig.full-screen` to display `content` from a datasource. The `isEditable` property is set to `true`, allowing the text in the web-view to be edited. An `execute-entity` action ensures the updated HTML is saved to the database.
{% endcolumn %}

{% column %}
Image\[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4yhXXgCmRFjbhuG8YuyU--20250519-104335.gif" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4yhXXgCmRFjbhuG8YuyU--20250519-104335.gif" size="66" width="681" height="1377" position="center" caption="Editable web-view" alt="Editable web-view"}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title=" web-view-edit.jigx" %}
```yaml
title: Notes
type: jig.full-screen
icon: notes-add

# Add the web-view component using the content property. 
# Set the isEditable property to true,
# to allow the HTML in the view to be edited by tapping the component.     
component: 
  type: component.web-view
  instanceId: edit-notes
  options:
    isEditable: true
    # Add HTML to the content, the HTML will be editable when tapped.
    content: |
      <!DOCTYPE html>
      <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Notes</title>
        <p><i>Add your notes here</i></p> 
# Configure an action to save the edited HTML to the database.       
actions:
    - children:
        - type: action.execute-entity
          options:
            title: Save notes
            provider: DATA_PROVIDER_DYNAMIC
            entity: default/jobs
            method: update
            goBack: stay
            data:
              id: =@ctx.datasources.work-notes.id
              job-notes: =@ctx.components.edit-notes.state.content
            # Confirm that the notes were saved successfully.  
            onSuccess:  
              type: action.info-modal
              options:
                modal:
                  element: 
                    type: icon
                    icon: check-2-alternate
                    color: positive
                  title: Notes added successfully
                  buttonText: Exit
```
{% endtab %}

{% tab title="datasource" %}
```yaml
datasources:
  work-notes: 
    type: datasource.sqlite
    options:
      isDocument: true
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - default/jobs
      query: 
        SELECT id,
         '$.job-notes',
         '$.job-number'
        FROM [default/jobs] 
        WHERE '$.job-number' =@jobNo
      queryParameters:
        jobNo: A1
```
{% endtab %}
{% endtabs %}
