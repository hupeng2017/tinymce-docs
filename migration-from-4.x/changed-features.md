---
layout: draft
title: Changed Features
title_nav: Changed Features
description: These features have either changed or have been deleted in TinyMCE 5.0.
keywords: deleted removed changedfeatures migration 4.x
---

Each release of TinyMCE adds new features and functionality. We also occasionally remove features and functionality, usually because we've added a better option.
Here are the details about the features and functionalities that we removed in Tiny 5.0.

## Removed Features

### Listbox

**Listbox** is no longer a supported toolbar button type in Tiny 5.0. Though listbox has been removed, any functionality provided by custom listbox toolbar buttons can be retained by switching to another type of toolbar button.
Any custom listbox toolbar buttons can be converted to a different type of toolbar button using the new API. The recommended toolbar button type to switch to is **Split** button.


## Removed Themes

### Inlite

The Inlite theme is no longer supported in Tiny 5.0. The features that the Inlite theme used to provide, is now available as a plugin. For a workaround, using the configuration parameter { theme: 'silver', inline: true, toolbar: false, plugins: [ 'inlite' ] },
will provide a similar and improved distraction free experience in Tiny 5.0.

### Modern

The Modern theme is no longer supported in Tiny 5.  The modern themes Ui library `tinymce.ui.*` are also deleted. This change may impact user depending upon their levels of custumization.
For a workaround, refer the following table:

| Customization Level | Description | Impact |
| ------------------- | ----------- | ------ |
| Minor | Has some custom buttons | no Ui fixes required, update button configuration to Tiny 5.0 format |
| Moderate | Has a webform in a dialog that can be submitted | port tiny 4 config to tiny 5 config |
| Major | You have created the kitchen sink | Not all api use cases are covered by our new Tiny 5 components, however we will strive to create a supprted work around or if there are sufficient requests, we will create a component to resolve the use case. |

> Note: Please provide feedback on your use case, and your current tinymce 4 configuration file containing only the ui component, you wish to have supported or to know a work around. -improve submission instructions -

> Note: The Silver theme in Tiny 5.0. contains a set of configuratable ui components, that could be used to replace the current customizations.



## Changed Features

### Table

* Styles text field has been removed from the advanced table of the dialogs. This simplifies the dialogs for users, and gives the editor stricter control over the table styles which means we are better able to ensure the styles are correct.
* Improved how styles are set and retrieved from tables, rows and cells, so this should be more reliable now.
* Shifted to using CSS more for styling, and therefore was able to remove a few legacy data attributes that we were setting on tables/rows/cells which are no longer good practice to use. This makes the output HTML cleaner and more modern.
* When opening a properties dialog with a single table/row/cell selected, the dialog will autofill with the relevant existing values. If you select multiple rows or cells and open the relevant properties dialog, Tiny 4 will leave all the dialog fields blank. In Tiny 5, any fields which have the same values for all the selected rows or cells will autofill, and the fields which have no existing value or have differing values will be empty.
* "Border" input field in the tableprops dialog is now called "Border width", for better clarity.

### Context Menu

The contextMenu can provide a simple list of clickable commands, or offer an in-menu form. This makes very simple attribute modification possible. Tiny 5.0 offers the contextMenu Plugin that is designed for web applications in need of menus on a possibly large amount of objects. Now, a single menu is defined that can be used by multiple objects and a contextMenu doesn't need to bind itself to triggering objects. This allows injecting and removing triggers without having to re-initialize or update contextMenu.
context menu release notes
- the context menu is no longer a plugin, it is part of the core and always enabled
- plugins can now register context menu sections
- editor `contextmenu` configuration can include menu items as before, but now also plugin menu sections
- e.g. the default context menu config is now `link image editimage table spelling` which are all plugin references


### Context Toolbar

The Context Toolbar configures its buttons based on the type of object selected in the Tree Outline. The Context Toolbar makes a limited number of relevant choices more visible and readily accessible.


#### Differences with TinyMCE 4

* buttons go before and after the input in t4 // TODO: resolve with align
* the Ctrl+K shortcut does nothing until the context toolbar is visible in t4. Possibly by design?
* In t5, the pop animates to its new width
* in t4, it is a url input, so you get a popup and a browse button. This might be something we have to implement, but it's not clear how to support it yet. I think at best for this release, we should just have before and after commands.

### Context Form

ContextForms are a generalisation of the `Insert Link` form that existed in the original `inlite` plugin from [TinyMCE 4]((https://www.tiny.cloud/docs/themes/inlite/#quicklink)).

### Toolbar buttons

Svg icons for better crisp look

New buttons are added to the global

* editor.buttons
* editor.menuItems
* editor.sidebar
* editor.contextToolbars


### Toolbar Menus

New buttons are added to the global `editor.settings.menus`

* Improvement -> now shows toggled state
* Improved mouse and keyboard nav




