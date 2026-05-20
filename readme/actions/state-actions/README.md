# State actions

Jigx provides three levels of _state management_ that allow you to store, update, and share data dynamically within your app.\
Each state type serves a different purpose, from app-wide variables to screen(jig)-specific and component-level data, enabling flexible logic and responsive UI behavior.

## **Types of State**

<table><thead><tr><th width="137.15234375">State Type</th><th width="146.31640625">Scope</th><th width="135.40234375">Defined In</th><th>Accessed Using</th><th>Typical Use Case</th></tr></thead><tbody><tr><td><a href="solution-state-set-and-reset.md">Solution State</a></td><td>Global (shared across all jigs)</td><td><code>index.jigx</code></td><td><code>@ctx.solution.state</code></td><td>Store user roles, preferences, or data shared across multiple screens.</td></tr><tr><td><a href="jig-state-set-and-reset.md">Jig State</a></td><td>Screen-specific</td><td>Inside a jig file (e.g., <code>jig-a.jigx</code>)</td><td><code>@ctx.jig-state</code></td><td>Manage temporary or screen-level logic, such as workflow steps or filters.</td></tr><tr><td><a href="set-state.md">State (Component State)</a></td><td>Component-specific</td><td>Within a component or control</td><td><code>@ctx.component.state</code><br><code>@ctx.current.state</code></td><td>Track component interactions, such as toggles, field input, or selected list items.</td></tr></tbody></table>

## **Best Practices**

* Use **Solution State** for global variables shared across multiple screens.
* Use **Jig State** for logic or UI control within a single screen.
* Use **Component State** for localized interactions within a specific component.
* Always reset state where appropriate (e.g., on logout, refresh, or workflow completion) to ensure consistent behavior.
