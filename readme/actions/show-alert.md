---
hidden: true
---

# show-alert

The `action.show-alert` provides a way to notify users about important information in your app,  you can choose to show the alert as a **toast** for lightweight updates, or a **modal** for important messages. Alerts can be customized with styling, icons, and interactive elements, allowing you to tailor them to different scenarios.

**Example use cases include:**

* **Error handling:** Display a retry prompt when a payment fails.
* **Login feedback:** Highlight invalid credentials or missing permissions.
* **Critical confirmations:** Require approval before deleting a record or submitting an expense.
* **Auto-dismiss** functionality for non-critical notifications.

## Configuration options

Some properties are common to all components, see [Common component properties](https://docs.jigx.com/examples/readme/actions/share) for a list and their configuration options.

<table><thead><tr><th width="140.36328125">Core Structure</th><th></th></tr></thead><tbody><tr><td>title</td><td>The main heading text displayed at the top of the alert. It should be concise and clearly state the purpose of the message.</td></tr><tr><td>presentAs</td><td><p>Specifies how the alert is presented to the user. Options include:</p><ul><li> <code>toast</code> (default):  For brief, lightweight notifications. </li><li><code>modal</code>: For important messages that require attention and may include additional information. Modal alerts are more disruptive since they block the UI and are typically used for critical information.</li></ul></td></tr></tbody></table>

<table><thead><tr><th width="139.98046875">Other options</th><th></th></tr></thead><tbody><tr><td><code>action</code></td><td>Interactive buttons or controls displayed within the alert let users respond or take specific actions. Use IntelliSense to see the list of available <a href="../../docs/Actions/">actions</a>.</td></tr><tr><td><code>description</code></td><td>The detailed message content that explains the alert’s purpose, provides instructions, or delivers additional information to the user.</td></tr><tr><td><code>dismiss</code></td><td><p>Configures how users can dismiss the alert. You can enable tap/gesture dismissal and set an automatic dismissal time.</p><ul><li><code>autoAfter</code> - specify the number of seconds after which the alert is automatically dismissed. Has no effect when <code>dismiss</code> is disabled.</li><li><code>isEnabled</code> - When set to <code>true</code> (default) a close (x) icon appears in the top-right corner of the alert, allowing manual dismissal. When set to <code>false</code>, the alert cannot be dismissed manually.</li></ul></td></tr><tr><td><code>group</code></td><td>Grouping allows you to manage multiple alerts under a shared identifier. This ensures that only one alert from a group is visible at a time, preventing alert overload and improving the user experience.<br><code>id</code> - Identifier for the alert group. Only one alert per group can be visible at a time. If a new alert with the same group ID is triggered while another is active, it will be skipped.</td></tr><tr><td><code>icon</code></td><td>The icon displayed alongside the alert content provides visual context and helps users recognize the alert’s type or purpose. The alert’s <code>style</code> property determines the icon color. If no style is set, the default <code>isWarning</code> style is applied.</td></tr><tr><td><code>style</code></td><td><p>Visual styling options let you set the tone of the alert:</p><ul><li><code>isPositive</code> (success/confirmation)</li><li><code>isNegative</code> (error) styling to convey the appropriate tone and urgency. </li><li><code>isWarning</code> (warning) styling is used by default.</li></ul></td></tr><tr><td><code>subtitle</code></td><td>Secondary text that appears below the <code>title</code>, providing additional context or supplementary information.</td></tr></tbody></table>

## Considerations

* [The `action.show-alert` is only available when used in an `onPress` event.](#user-content-fn-1)[^1]

## Examples and code snippets

### Show-alert as a toast



### Show-alert as a modal



### Show-alert with actions



### Show-alert with styling



### Show-alert with icons and styling



### Show-alert with automatic dismissal



### Show-alert with group id



### Show-alert in a banner ????



### Show-alert in a REST function

[^1]: This cannot be right? Why can i not see it in Intelliscence in actions??
