# Events

Events trigger actions that respond to user interactions or system changes. They enable dynamic app behavior by executing specific functions when conditions are met. By leveraging events, you can enhance user experience, automate processes, and ensure seamless data synchronization within the app. The following events are configurable:

<table isTableHeaderOn="true" selectedColumns="" selectedRows="" selectedTable="false" columnWidths="151">
  <tr>
    <td selected="false" align="left">
      <p><strong>Event</strong></p>
    </td>
    <td selected="false" align="left">
      <p><strong>Description</strong></p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onFocus</code></p>
    </td>
    <td selected="false" align="left">
      <p><code>onFocus</code> triggers when a solution or jig gains focus, meaning it becomes the active element the user is interacting with. It is used to refresh data, adjust UI behavior, or trigger actions when the user returns to a screen.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onLoad</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>onLoad</code> event is triggered when the solution loads in the app. It is commonly used to initialize data, fetch remote resources, or set up UI elements before the user interacts with the solution.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onPress</code></p>
    </td>
    <td selected="false" align="left">
      <p>This event is triggered when a user taps on a certain UI element, such as a button, link, or interactive component. It is used to handle user interactions and execute specific actions based on the tap event.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><code>onRefresh</code></p>
    </td>
    <td selected="false" align="left">
      <p>The <code>onRefresh</code> event is triggered when the user performs a refresh action, typically by pulling down on a list or screen. It is commonly used to reload data from a remote source or update displayed content to reflect the latest changes.</p>
    </td>
  </tr>
  <tr>
    <td selected="false" align="left">
      <p><a href="./Events/onTableChange.md">onTableChanged</a> </p>
    </td>
    <td selected="false" align="left">
      <p>This event checks for local data changes within the app on specific data tables (entities). When a change is detected, the event triggers the configured actions that call remote data providers to sync and apply those changes. This ensures that the local and remote data stay consistent, maintaining up-to-date information across the system.</p>
    </td>
  </tr>
</table>

