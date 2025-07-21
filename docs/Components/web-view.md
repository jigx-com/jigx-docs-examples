# web-view

This component displays a webpage from a specified URL, content from a datasource, or custom HTML.

:::hint{type="info"}
You can also use the [jig.document](<./../Jig Types/jig_document.md>) type to display web pages in full-screen mode or pass messages from your HTML content via JavaScript to the Jigx App.
:::

## Configuration options

Some properties are common to all components, see [Common component properties](docId\:LLnTD-rxe8FmH7WpC5cZb) for a list and their configuration options.

| **Core structure** |                                                                 |
| ------------------ | --------------------------------------------------------------- |
| `uri`              | The source to be displayed in the web-view, for example, a URL. |

| **Other options**                |                                                                                                                                                                                                                                                                          |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `content`                        | HTML to render in the web-view.                                                                                                                                                                                                                                          |
| `height`                         | The height of the web-view.                                                                                                                                                                                                                                              |
| `isEditable`                     | A very basic implementation, if set to `true`, the web-view `content` becomes editable. This works only with `content`, not with a `uri`. The `isEditable` property is only available when using the web-view in a [jig.fullscreen](<./../Jig Types/jig_fullscreen.md>). |
| `isTrackingTransparencyRequired` | If set to `true` tracking transparency permission modal is shown before opening the URL. The default setting is `true`.                                                                                                                                                  |

## Consideration

- The `component.web-view` can be used in [jig.fullscreen](<./../Jig Types/jig_fullscreen.md>), if the content needs to fill the screen.

## Examples and code snippets

:::::ExpandableHeading

### Web-view example (URL)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VeM3NrBpP0oAm20xE_SLn_img9582iphone13blueportrait.png" size="80" position="center" caption="Web-view with URL " alt="Web-view with URL " signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/VeM3NrBpP0oAm20xE_SLn_img9582iphone13blueportrait.png"}
:::

:::VerticalSplitItem
In this example, we open a target URL in the web-view component.

If the target URL is tracking data (e.g., cookies etc.), you are required by Apple to ask for user consent using the `isTrackingTransparencyRequired` option. It will ask for user consent the first time any web view in your solution tries to open a target URL.

**Examples**:
See the full example using static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/web-view/static-data/web-view-example/web-view-example.jigx).
See the full example using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jigx-components/web-view/dynamic-data/web-view-example-dynamic/web-view-example-dynamic.jigx).

**Datasource**:
See the full datasource for static data on [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/web-view.jigx).
See the full datasource for dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/datasources/adhoc-components/web-view-dynamic.jigx).
:::
::::

:::CodeblockTabs
web-view (static)

```yaml
type: jig.default
title: Web view

children:
  - type: component.web-view
    options:
      uri: =@ctx.datasources.web-view.url
      isTrackingTransparencyRequired: true
```

web-view (dynamic)

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

datasources (static)

```yaml
datasources:
  web-view:
    type: datasource.static
    options:
      data:
        - url: https://www.jigx.com
```

datasources (dynamic)

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
        FROM [default/links] WHERE '$.category' = "web-view"
```

:::
:::::

:::::ExpandableHeading

### Web-view example (HTML Content)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/iUGy63w8idJuWWfsn9RKv_img9581iphone13blueportrait.png" size="80" position="center" caption="Web-view with HTML content" alt="Web-view with HTML content" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/iUGy63w8idJuWWfsn9RKv_img9581iphone13blueportrait.png"}
:::

:::VerticalSplitItem
In this example, we are passing raw HTML content to the web-view component. This can either be inline content (see example below) or content from a datasource.
If your HTML content does not render as expected (e.g. font too small etc.) embed the meta HTML tag used in the example below in your HTML content.
:::
::::

:::CodeblockTabs
web-view-raw

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

:::
:::::

:::::ExpandableHeading

### Editable web-view content (Fullscreen)

::::VerticalSplit{layout="middle"}
:::VerticalSplitItem
In this example, the web-view component is used to make notes on a job. It is configured in a `jig.full-screen` to display `content` from a datasource. The `isEditable` property is set to `true`, allowing the text in the web-view to be edited. An `execute-entity` action ensures the updated HTML is saved to the database.
:::

:::VerticalSplitItem
::Image[]{src="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4yhXXgCmRFjbhuG8YuyU--20250519-104335.gif" signedSrc="https://archbee-image-uploads.s3.amazonaws.com/0TQnKgJpsWhT3gQzQOhdY-4yhXXgCmRFjbhuG8YuyU--20250519-104335.gif" size="66" width="681" height="1377" position="center" caption="Editable web-view" alt="Editable web-view"}
:::
::::

:::CodeblockTabs
web-view-edit.jigx

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

datasource

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

:::
:::::
