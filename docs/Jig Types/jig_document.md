# jig.document

{% columns %}
{% column %}
The document jig type is used to display documents connected to your solution. The display of the document is provided in the following formats:

1. PDF file
2. HTML page - set up using:
   1. A URL (website link)
   2. HTML&#x20;
{% endcolumn %}

{% column %}
&#x20;![Jig Document Preview](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/JLby7gG3QE9amF9juIjOB_document.png)


{% endcolumn %}
{% endcolumns %}

### Configuration options

Some properties are common to all jig types, see [Common jig type properties](jig_document.md) for a list and their configuration options.

<table><thead><tr><th width="146.35546875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>title</code></td><td>Provide the name of the screen. If you do not want to show a title in a jig use <code>title: ' '</code> or add an expression.</td></tr><tr><td><code>source</code></td><td>Select from <code>PDF</code> or <code>HTML</code> content.</td></tr></tbody></table>

<table><thead><tr><th width="147.6171875">Other options</th><th></th></tr></thead><tbody><tr><td><code>description</code></td><td>The general description of the document.</td></tr><tr><td><code>badge</code></td><td>Enhance your widget with customizable badges, for instance, show the number of documents. Add the <code>badge</code> property to the jig YAML with an expression.</td></tr><tr><td><code>icon</code></td><td>The icon will be displayed on the widget of this jig. Start typing the name of the icon to invoke the available list in IntelliSense. See <a href="jig_document.md">Jigx icons</a> for information on working with icons.</td></tr><tr><td><code>placeholders</code></td><td>Create a placeholder to show when there is no data to use yet. See tips and tricks -use a placeholder for a placeholder example.</td></tr></tbody></table>

### Examples and code snippets

{% hint style="success" %}
The code below is an extract from the full _jigx-samples_ solution. The code snippets describe the component discussed in this section. For the solution to function in the Jigx app download the full _jigx-samples_ project from :Link\[GitHub]{href="https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples" newTab="true" hasDisabledNofollow="false"}, and follow the instructions in [Setting up your solution](jig_document.md).
{% endhint %}

#### PDF Document Example

{% columns %}
{% column %}
&#x20;![PDF document jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/1TFIe7dRl7t_4htbo1Zck_ksh-eh642hpw7uszthpedocument-pdfiphone13blueportrait.png)&#x20;


{% endcolumn %}

{% column %}
This example displays a `Document Jig` used to display a `PDF document`.

**Examples**: \
See the full code sample using static data in [GitHub](jig_document.md) See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-document/dynamic-data/document-pdf-dd.jigx).

{% hint style="success" %}
Using the code below requires data in the database, the jigx.sample solution has the data provided for documents. You can use the documents.csv file in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/csv/documents.csv) and upload it via the [Data](jig_document.md) configuration in Jigx Management.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="document-pdf-dd.jigx" %}
```yaml
type: jig.document
title: PDF Document Type (Dynamic Data)
description: Example of PDF Financial Report
icon: document
badge: 1

placeholders:
  - when: =@ctx.system.isOffline
    title: No data to display
  
source:
  documentType: PDF
  uri:  =@ctx.datasources.documents-dynamic[type='PDF'].url
```
{% endtab %}

{% tab title="datasources" %}
```yaml
datasources:
  documents-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/documents
      query: |
        SELECT 
          id, 
          '$.name', 
          '$.description', 
          '$.type', 
          '$.url' 
        FROM [default/documents] 
```
{% endtab %}

{% tab title="default.jigx" %}
```yaml
databaseId: default
tables:
  documents: null
```
{% endtab %}

{% tab title="index.jigx" %}
```yaml
name: jig-doc-pdf
title: jig-doc-examples
category: business
tabs:
  home:
    jigId: document-pdf-dd
    icon: home-apps-logo
```
{% endtab %}
{% endtabs %}

#### HTML Document Example (URL)

{% columns %}
{% column %}
&#x20;![HTML Document jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/BvMH_mkZJ_idMyXtQlDVO_5zwbzha-ohev7arducssfdocument-htmliphone13blueportrait.png)&#x20;


{% endcolumn %}

{% column %}
In this example a `jig.document` is used to display an `HTML` document.

**Examples:**\
See the full code sample using static data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-document/static-data/document-html-url-sd.jigx). See the full code sample using dynamic data in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-document/dynamic-data/document-html-url-dd.jigx).

{% hint style="success" %}
Using the code below requires data in the database, the jigx.sample solution has the data provided for documents. You can use the documents.csv file in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/csv/documents.csv) and upload it via the [Data](jig_document.md) configuration in Jigx Management.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="document-html-dd.jigx" %}
```yaml
type: jig.document
title: HTML Document Type (Dynamic Data)
description: Example of Business Offers via HTML url
icon: document
badge: 1

placeholders:
  - when: =@ctx.system.isOffline
    title: No data to display

source:
  documentType: HTML
  uri:  =@ctx.datasources.documents-dynamic[type='HTML'].url
```
{% endtab %}

{% tab title="datasources" %}
```yaml
datasources:
  document-dynamic:
    type: datasource.sqlite
    options:
      provider: DATA_PROVIDER_DYNAMIC
      entities:
        - entity: default/documents
      query: |
        SELECT 
          id, 
          '$.name', 
          '$.description', 
          '$.type', 
          '$.url' 
        FROM [default/documents] 
```
{% endtab %}

{% tab title="default.jigx" %}
```yaml
databaseId: default
tables:
  documents: null
```
{% endtab %}

{% tab title="index.jigx" %}
```yaml
name: jig-doc-html
title: jig-doc-examples
category: business
tabs:
  home:
    jigId: document-html-dd
    icon: home-apps-logo
```
{% endtab %}
{% endtabs %}

#### HTML Document Example (Content)

You can also use this jig type to pass raw HTML into the webview (without linked CSS, JS etc.).

{% hint style="info" %}
If your HTML content does not render as expected e.g. font too small, embed this HTML tag in your HTML content that you are passing into the uri option.
{% endhint %}

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

{% columns %}
{% column %}
&#x20;![HTML Document jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/2-hef4bxogjQfpMVrfRIe_document-content.PNG)
{% endcolumn %}

{% column %}
In this example a `jig.document` is used to display raw HTML content.

**Examples:**\
See the full code sample in [GitHub](https://github.com/jigx-com/jigx-samples/blob/main/quickstart/jigx-samples/jigs/jig-types/jig-document/static-data/document-html-content.jigx).
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="document-html-content.jigx" %}
```yaml
title: HTML Document Type (Content)
type: jig.document

source:
  documentType: HTML
  content: |
      <html>
        <head>
          <meta name="viewport" content="width=device-width, initial-scale=1">
        </head>
        <body style="margin: 0;text-align: center;">
         <img src="https://www.jigx.com/wp-content/uploads/2023/05/MSGraph01.png" alt="Jigx website screenshot"
        style="max-width: 100vw; height: 100vh; ">
        </body>
      </html>
```
{% endtab %}

{% tab title="index.jigx" %}
```yaml
name: jig-html-content
title: jig-html-content
category: business
tabs:
  home:
    jigId: document-html-content
    icon: home-apps-logo
```
{% endtab %}
{% endtabs %}

#### HTML Document Example (Content with Message Listener)

{% columns %}
{% column %}
&#x20;![HTML Document jig](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/Nd9RXpf3nHjf4FZLITiKG_img5019a1d0eb6f-1iphone13blueportrait.png)


{% endcolumn %}

{% column %}
In this example a `jig.document` is used to display raw HTML content. A message listener was added via JavaScript called `linkTapped()`. The HMTL can pass a value into the message listener and the message then gets passed on as JSON to the Jigx App . The JSON object is then available in the state expression using `@ctx.jig.state.data`. All properties of your object can be accessed using `@ctx.jig.state.data.[yourproperty]`.

When the jig gets focus, the state is reset in this example.

{% hint style="info" %}
This code example is **not** in the jigx.samples solution in GitHub.
{% endhint %}
{% endcolumn %}
{% endcolumns %}

{% tabs %}
{% tab title="document-htmlcontent-listener.jigx" %}
```yaml
title: "=$boolean(@ctx.jig.state.data) ? @ctx.jig.state.data.message : 'Tap on the link'"
type: jig.document

onFocus: 
  type: action.reset-state
  options:
    state: =@ctx.jig.state.data

source: 
  documentType: HTML
  isTrackingTransparencyRequired: false
  content: |
    <html>
      <head>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <script language="javascript">
          function linkTapped(val)
          {
            window.ReactNativeWebView.postMessage(JSON.stringify({message : val}));
          }
        </script>
      </head>
      <body>
        <a href="javascript:linkTapped('Hello World')">Tap me</a>
      </body>
    </html>
```
{% endtab %}

{% tab title="index.jigx" %}
```yaml
name: jig-html-content-listener
title: jig-html-listener
category: business
tabs:
  home:
    jigId: document-htmlcontent-listener
    icon: home-apps-logo
```
{% endtab %}
{% endtabs %}

## See Also

* [Jigs (screens)](jig_document.md)
* [Related examples (Github)](https://github.com/jigx-com/jigx-samples/tree/main/quickstart/jigx-samples/jigs/jig-types/jig-composite)
