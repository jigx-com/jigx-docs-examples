# find-replace

The find-replace action enables data manipulation, you programmatically search for and replace string values within your local data or Dynamic data tables. This action provides an efficient way to bulk update data across rows and columns without manual intervention.

### What is the Find-Replace Action?

The find-replace action enables you to perform string substitutions across your local data tables, including DD (Dynamic Data) tables and tables populated through webhooks or other data sources. When you execute a find-replace operation, the system searches for specific string values and replaces them with new values throughout the selected dataset.

### Key Capabilities

**Local Data Updates**: The action works seamlessly with your local data tables, allowing you to modify content that resides within your Jigx application environment.

**Dynamic Data Integration**: One of the most significant features is its ability to work with DD tables. When you make changes using find-replace, these modifications are automatically propagated back to the Dynamic Data, eliminating the need to manually queue updates.

**Bulk Text Operations**: Instead of editing individual records, you can perform sweeping changes across entire datasets. For example, you could replace all instances of "dog-products" with "pet-products" across a products table in a single operation.

**Real-time Synchronization**: Changes made through the find-replace action are immediately reflected in your local tables and can be synchronized with upstream data sources like Dynamic Data using execute-entities and functions.

### Use Cases

The find-replace action is particularly valuable for:

* **Data Standardization**: Correcting inconsistent naming conventions or formatting across large datasets.
* **Content Updates**: Updating company names, product names, or other information that appears multiple times.
* **Data Migration**: Cleaning and transforming data during system transitions.
* **Batch Corrections**: Fixing systematic errors or typos across multiple records.

### Integration with Jigx Ecosystem

This action works as part of Jigx's broader table [operations](https://docs.jigx.com/building-apps-with-jigx/data/data-providers/rest/functions/operations) framework, complementing other data manipulation tools and maintaining consistency with your overall data management workflow. Whether your data comes from Dynamic Data tables, webhook integrations, REST or other sources, the find-replace action provides a unified approach to string-based modifications.

## Configuration options

<table><thead><tr><th width="152.64453125">Core structure</th><th></th></tr></thead><tbody><tr><td><code>find</code></td><td>The string value to be searched for in the tables.</td></tr><tr><td><code>replace</code></td><td>The string value to replace the found value with in the tables.</td></tr><tr><td><code>tables</code></td><td>The tables in which the string value is searched for and replaced. </td></tr></tbody></table>

<table><thead><tr><th width="214.0859375">Other options</th><th></th></tr></thead><tbody><tr><td><code>icon</code></td><td>Select an to display when the action is configured as the secondary button or in a <a href="../../docs/Components/jig-header.md">header action</a>.</td></tr><tr><td><code>includeCommandQueue</code></td><td>If set to <code>false</code>, the command queue will not be included in the find and replace.</td></tr><tr><td><code>isHidden</code></td><td><code>true</code> hides the action button, <code>false</code> shows the action button. Default setting is <code>false</code>.</td></tr><tr><td><code>style</code></td><td><ul><li><code>isDanger</code> - Styles the action button in red or your brand's designated danger color.</li><li><code>isDisabled</code> - Displays the action button as greyed out, preventing the button from being actioned.</li><li><code>isPrimary</code> - Styles the action button in blue or your brand's designated primary color.</li><li><code>isSecondary</code> - Sets the action as a secondary button, accessible via the ellipsis. The <code>icon</code> property can be used when the action button is displayed as a secondary button.</li></ul></td></tr></tbody></table>

## Considerations

* **Use with Caution**: The find-replace action requires careful consideration before execution. When you perform a find-replace operation, the data is replaced for every instance found throughout the specified tables. This means that all matching values will be modified simultaneously, which could have unintended consequences if not properly planned. Before executing a find-replace operation, it's recommended to:
  * Carefully review the scope of tables that will be affected
  * Consider creating backups of critical data
  * Test the operation on a smaller dataset first if possible
  * Verify that the replacement value won't create conflicts or inconsistencies elsewhere in your data

## Examples and code snippets

