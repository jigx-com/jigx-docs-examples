---
title: Actions
slug: gu-O-actions
createdAt: Wed Jan 17 2024 10:25:09 GMT+0000 (Coordinated Universal Time)
updatedAt: Fri Mar 14 2025 09:00:12 GMT+0000 (Coordinated Universal Time)
---

Refer to the [actions]() topic to understand concepts such as local and global actions, types of actions, as well as, how and where to configure actions in jigs, and data. The topics in this section provide code examples for each action.

Adding an `icon` property in an action* *only applies to `swipeable`, `secondary`, and `header` actions. Primary actions do not support icon setups.

Here is a list of all actions and the category type the action forms part of.

| **Type**   | **Description**                                                                                                                  | **Action**                                                                                                                                                                                    |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Execution  | Actions used to interact with data.                                                                                              | [execute-entity](./Actions/execute-entity.md)                                                                                                                                                 |
|            |                                                                                                                                  | [execute-entities](./Actions/execute-entities.md)                                                                                                                                             |
|            |                                                                                                                                  | [submit-form](./Actions/submit-form.md)                                                                                                                                                       |
|            |                                                                                                                                  | [sync-entities](./Actions/sync-entities.md)                                                                                                                                                   |
|            |                                                                                                                                  | [print](./Actions/print.md)                                                                                                                                                                   |
|            |                                                                                                                                  | [generate-pdf](./Actions/generate-pdf.md)                                                                                                                                                     |
|            |                                                                                                                                  | [generate-file](./Actions/generate-file.md)                                                                                                                                                   |
|            |                                                                                                                                  | [share](./Actions/share.md)                                                                                                                                                                   |
|            |                                                                                                                                  | [update-profile](./Actions/update-profile.md)                                                                                                                                                 |
| Navigation | Actions used to navigate to another jig or Home Hub                                                                              | [go-to](./Actions/go-to.md)<br />                                                                                                                                                             |
|            |                                                                                                                                  | [go-back](./Actions/go-back.md)                                                                                                                                                               |
|            |                                                                                                                                  | [set-active-tab](./Actions/set-active-tab.md)                                                                                                                                                 |
| Opening    | Actions used to *open* certain [Components](./Components.md).                                                                    | [open-map](./Actions/open-map.md)                                                                                                                                                             |
|            |                                                                                                                                  | [open-media-picker](./Actions/open-media-picker.md)                                                                                                                                           |
|            |                                                                                                                                  | [open-scanner](./Actions/open-scanner.md)                                                                                                                                                     |
|            |                                                                                                                                  | [open-url](./Actions/open-url.md)                                                                                                                                                             |
| Evaluation | *Evaluation state -* actions to determine a specific status or value of a solution, property, or component.                      | [set-state](./Actions/set-state.md)                                                                                                                                                           |
|            |                                                                                                                                  | [reset-state](./Actions/reset-state.md)                                                                                                                                                       |
| Grouping   | Multiple actions can be grouped to run with a single user interaction. The actions can be run sequentially or executed in bulk.  | [action-list](./Actions/action-list.md)                                                                                                                                                       |
| Display    | Action used to display a modal or popup containing a message.                                                                    | [confirm](./Actions/confirm.md)&#xA;[info-modal](./Actions/info-modal.md)                                                                                                                     |
| Events     | Actions that execute after a user or device performs a trigger.                                                                  | - onRefresh
- onFocus
- onPress
- onLoad (only on index.jigx)
- onChange
- onDelete
- onButtonPress (only on calendar jigs)
- [onTableChange](./Events/onTableChange.md) (only on index.jigx) |



