---
hidden: true
---

# banner

{% columns %}
{% column %}
The **Banner component** provides a flexible way to deliver important messages directly within your mobile app. Designed to support icons, styled text, and action buttons, it can be customized to match your app’s look and feel. Use banners to highlight errors, warnings, or information, as well as to drive user action with clear calls to action. Whether alerting field workers to an issue, sharing status updates, or prompting the next step, banners ensure critical information is visible, actionable, and consistent with your design requirements.
{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

## Configuration options

<table><thead><tr><th width="152.23046875">Core structure</th><th></th></tr></thead><tbody><tr><td><code>instanceId</code></td><td>The <code>instanceId</code> is a unique identifier assigned to the banner component. It allows other parts of the app—such as functions, actions, or conditional logic—to reference this specific banner. By using the <code>instanceId</code>, you can programmatically control when the banner is shown or hidden, update its content dynamically, or trigger interactions tied to that particular instance. This ensures that each banner can be distinctly managed, even when multiple banners are present on the same screen.</td></tr><tr><td><code>title</code></td><td>The <code>title</code> property defines the main text displayed in the banner. It supports multiple configuration options; you can provide a static string, bind it dynamically using an expression, or extend it with <code>line options</code> for advanced styling. With <code>line options</code>, you can control text appearance using properties such as <code>fontSize</code>, <code>isbold</code>, and <code>color</code>, as well as specify the <code>numberOfLines</code> to display. </td></tr><tr><td><code>when</code></td><td>The <code>when</code> property controls the visibility of a component by evaluating a condition. When the condition resolves to <code>true</code>, the component is displayed; when it resolves to <code>false</code>, the component is hidden. This allows you to show or hide any component dynamically based on expressions, data values, or user interactions.</td></tr></tbody></table>

<table><thead><tr><th width="161.953125">Other options</th><th></th></tr></thead><tbody><tr><td><code>leftElement</code></td><td>The <code>leftElement</code> property lets you add an icon to the left side of the banner, providing a visual cue that reinforces the banner’s purpose—for example, signaling an error, warning, or informational message. The icon can be fully customized using styling options such as <code>type</code> (duotone, contained, or basic), <code>shape</code> (rounded, circle, or basic), and <code>color</code> to align with your app’s design. Additionally, you can make the icon interactive by configuring an <code>onPress</code> property to trigger an action when the icon is tapped.</td></tr><tr><td><code>style</code></td><td>The <code>styling</code> property defines the visual appearance of the banner based on the type and importance of the message. It provides preset styling options—<code>isPositive</code>, <code>isNegative</code>, and <code>isWarning</code>—to help communicate success, errors, or caution at a glance. By applying the appropriate style, you can ensure that users immediately recognize the context and urgency of the message being displayed.</td></tr><tr><td><code>subtitle</code></td><td>The <code>subtitle</code> property defines the secondary text displayed beneath the banner’s title. It offers flexible configuration options; you can provide a static string, bind the value dynamically with an expression, or enhance it using <code>line options</code> for advanced styling. With <code>line options</code>, you can customize the text’s appearance using properties such as <code>fontSize</code>, <code>isBold</code>, and <code>color</code>, and control layout by specifying <code>numberOfLines</code>. </td></tr></tbody></table>

<table><thead><tr><th width="169.9375">Actions</th><th></th></tr></thead><tbody><tr><td><code>actions</code></td><td>The <code>action</code> property defines what happens when the banner’s action button is tapped. You can configure it to trigger any supported app action—such as navigating to another screen, opening a URL, or updating data. Use IntelliSense to explore the full list of available actions.  </td></tr></tbody></table>

<table><thead><tr><th width="190.0078125">State configuration</th><th width="152.046875">Key</th><th>Notes</th></tr></thead><tbody><tr><td>=@ctx.solution.state.</td><td>status</td><td>Global state variable that can be used throughout the solution.</td></tr><tr><td>=@ctx.jig.state.</td><td>activeItem<br>filter<br>searchText</td><td>Jig-level state that applies to the specific jig (screen) context, with available keys depending on the jig type (e.g., for list jigs: activeItem, filter, searchText, etc.)</td></tr></tbody></table>

## Considerations

*

## Examples and code snippets

### Basic banner

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}



### Banner with actions

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

### Banner with one action

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

### Banner with an icon

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

### Banner with icon onPress

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

### Banner with icon and actions

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

### Banner with styling

{% columns %}
{% column %}

{% endcolumn %}

{% column %}

{% endcolumn %}
{% endcolumns %}

