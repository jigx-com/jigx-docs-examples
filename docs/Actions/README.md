---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Actions

Refer to the [actions](https://docs.jigx.com/building-apps-with-jigx/ui/actions) topic to understand concepts such as local and global actions, types of actions, as well as, how and where to configure actions in jigs, and data. The topics in this section provide code examples for each action.

Adding an `icon` property in an action only applies to `swipeable`, `secondary`, and `header` actions. Primary actions do not support icon setups.

Here is a list of all actions and the category type the action forms part of.

<table><thead><tr><th width="153.4609375">Type</th><th width="338.54296875">Description</th><th>Action</th></tr></thead><tbody><tr><td>Execution</td><td>Actions used to interact with data.</td><td><a href="execute-entity.md">execute-entity</a></td></tr><tr><td></td><td></td><td><a href="execute-entities.md">execute-entities</a></td></tr><tr><td></td><td></td><td><a href="execute-sql.md">execute-sql</a></td></tr><tr><td></td><td></td><td><a href="submit-form.md">submit-form</a></td></tr><tr><td></td><td></td><td><a data-mention href="../../readme/actions/find-replace.md">find-replace.md</a></td></tr><tr><td></td><td></td><td><a href="sync-entities.md">sync-entities</a></td></tr><tr><td></td><td></td><td><a href="print.md">print</a></td></tr><tr><td></td><td></td><td><a href="generate-pdf.md">generate-pdf</a></td></tr><tr><td></td><td></td><td><a href="generate-file.md">generate-file</a></td></tr><tr><td></td><td></td><td><a href="share.md">share</a></td></tr><tr><td></td><td></td><td><a href="update-profile.md">update-profile</a></td></tr><tr><td>Navigation</td><td>Actions used to navigate to another jig or Home Hub</td><td><a href="go-to.md">go-to</a></td></tr><tr><td></td><td></td><td><a href="go-back.md">go-back</a></td></tr><tr><td></td><td></td><td><a href="set-active-tab.md">set-active-tab</a></td></tr><tr><td>Opening</td><td>Actions used to <em>open</em> certain <a href="Components.md">Components</a>.</td><td><a href="open-map.md">open-map</a></td></tr><tr><td></td><td></td><td><a href="open-media-picker.md">open-media-picker</a></td></tr><tr><td></td><td></td><td><a href="open-scanner.md">open-scanner</a></td></tr><tr><td></td><td></td><td><a href="open-url.md">open-url</a></td></tr><tr><td>Evaluation</td><td><em>Evaluation state -</em> actions to determine a specific status or value of a solution, property, or component.</td><td><a href="set-state.md">set-state</a></td></tr><tr><td></td><td></td><td><a href="reset-state.md">reset-state</a></td></tr><tr><td>Grouping</td><td>Multiple actions can be grouped to run with a single user interaction. The actions can be run sequentially or executed in bulk.</td><td><a href="action-list.md">action-list</a></td></tr><tr><td>Display</td><td>Action used to display a modal or popup containing a message.</td><td><a href="confirm.md">confirm</a><br><a href="info-modal.md">info-modal</a></td></tr><tr><td>Events</td><td>Actions that execute after a user or device performs a trigger.</td><td><ul><li>onRefresh</li><li>onFocus</li><li>onPress</li><li>onLoad (only on index.jigx)</li><li>onChange</li><li>onDelete</li><li>onButtonPress (only on calendar jigs)</li><li><a href="../Events/onTableChange.md">onTableChange</a> (only on index.jigx)</li></ul></td></tr><tr><td><p>Reuse</p><p>(<a href="https://docs.jigx.com/building-apps-with-jigx/ui/actions#global-actions">global-actions</a>)</p></td><td>Using the <code>execute-action</code> action provides greater control and enables reuse when the same logic needs to be performed in multiple places. For example, <code>action.sync-entities</code> might be called during app initialization, again when data changes, or when only a specific subset of data needs to be synced. By using <code>execute-action</code>, you can easily reuse the granular actions that handle the actual work, reducing duplication and improving maintainability.</td><td>execute-actions</td></tr></tbody></table>
