# interactive-image

An interactive image has clickable links that can be used in various ways. For instance, it can be clicked on to reveal information about a specific point, indicate a selection, such as a booking, or use it as a multi-selection. This is typically used when the information you need to convey is better presented visually than in text.&#x20;

![Interactive images](https://archbee-image-uploads.s3.amazonaws.com/x7vdIDH6-ScTprfmi2XXX/OZ2ahxGqIKn7vTYf5BExY_cc-interactiveimage.png "Interactive images")

## Configuration options

Some properties are common to all components, see [Common component properties]() for a list and their configuration options.

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="123">
  <tr>
    <td selected="false" align="left">
      <p><strong>Core structure</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>source</code></p>
    </td>
    <td selected="false" align="left">
      <p>The image source can be a remote URL or a local file resource. This property can also contain several remote URLs, specified with their width and height and potentially with scale/other URI arguments. The native side will then choose the best uri to display based on the measured size of the image container.
      The currently supported formats are png, jpg, jpeg, bmp, gif, webp (Android only), psd (iOS only).</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>body</code></p>
    </td>
    <td selected="false" align="left">
      <p>The HTTP body to send with the request. This must be a valid UTF-8 string, and will be sent exactly as specified, with no additional encoding (e.g. URL-escaping or base64) applied.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>bundle</code></p>
    </td>
    <td selected="false" align="left">
      <p>The iOS asset bundle which the image is included in. This will default to [NSBundle mainBundle] if not set.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>cache</code></p>
    </td>
    <td selected="false" align="left">
      <p>A <code>cache</code> property can be added to control how networked requests interact with the local cache.</p>
      <ul>
      <li><code>default</code>: Use the native platforms default strategy.</li>
      <li><code>useProtocolCachePolicy</code> on iOS.</li>
      <li><code>force-cache</code>: The existing cached data will be used to satisfy the request, regardless of its age or expiration date. If there is no existing data in the cache corresponding the request, the data is loaded from the originating source.</li>
      <li><code>only-if-cached</code>: The existing cache data will be used to satisfy a request, regardless of its age or expiration date. If there is no existing data in the cache corresponding to a URL load request, no attempt is made to load the data from the originating source, and the load is considered to have failed.</li>
      <li><code>reload</code>: The data for the URL will be loaded from the originating source. No existing cache data should be used to satisfy a URL load request.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>headers</code></p>
    </td>
    <td selected="false" align="left">
      <p>The object representing the HTTP headers to send along with the request for a remote image.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>height</code></p>
    </td>
    <td selected="false" align="left">
      <p>The height of the source.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>method</code></p>
    </td>
    <td selected="false" align="left">
      <p>The HTTP Method to use. Defaults to GET if not specified.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>scale</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>scale</code> is used to indicate the scale factor of the image. Defaults to 1.0 if unspecified, meaning that one image pixel equates to one display point / DIP.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>uri</code></p>
    </td>
    <td selected="false" align="left">
      <p>Uri for the image, can be string or Jigx expression.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>width</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>width</code> and <code>height</code> can be specified if known at build time, in which case these will be used to set the default image component dimensions.</p>
    </td>
  </tr>
</table>

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="127">
  <tr>
    <td selected="false" align="left">
      <p><strong>Other options</strong></p>
    </td>
    <td selected="false" align="left">
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>data</code></p>
    </td>
    <td selected="false" align="left">
      <p>Provide the x and y coordinates to be placed on the image.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>groups</code></p>
    </td>
    <td selected="false" align="left">
      <p>This property includes <code>title</code> and <code>id</code>, with the additional option of adding a <code>color</code> for your group and <code>maximumPoints</code>, which defines the maximum possible number of selected points. The <code>groups</code> property is used to specify certain groups to distinguish between selected/unselected and otherwise specified areas.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>imageHeight</code></p>
    </td>
    <td selected="false" align="left">
      <p>The height of the image is specific. If the height is bigger than the image ratio (width/height), the height is correlated based on the image dimensions.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>item</code></p>
    </td>
    <td selected="false" align="left">
      <p>There is only one available option, which is .</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>pointColor</code></p>
    </td>
    <td selected="false" align="left">
      <p>The color of the point(s) marked on the image. The default color for point items is inactive state.</p>
    </td>
  </tr>
</table>

## Considerations

- The interactive component serves as a container for the [interactive-image-item](./interactive-image/interactive-image-item.md) component.
- The images can be preloaded and cached using the asset folder's images file. The images will be displayed even when you are offline. For more details, refer to [Assets](https://docs.jigx.com/assets).

