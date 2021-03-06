---
layout: default
title: Overview
title_nav: Overview
description: This section shows you how to add a custom button to the Tiny 5.0 toolbar.
keywords: toolbar toolbarbuttons buttons toolbarbuttonsapi
---

## Use Cases

* Create a shortcut for some action/series of actions that the user does often/repeatedly.
* Create a button for some custom behaviour.

## Types of Toolbar Buttons

### Basic Button

A basic button simply triggers it's `onAction` function when clicked. For more information, see [Basic Button]({{site.baseurl}}../component/basic).

### Toggle Button

A toggle button, when clicked, triggers an action like a basic button, but it also has a concept of state, and can be toggled on and off. Toggle buttons have CSS styling to show their state, which gives the user visual feedback. 

> Example: Bold button, which gets highlighted if your cursor is in a word with bold formatting.
For more information, see [Toggle Button]({{site.baseurl}}../component/toggle).

### Split Button

A split button (also called a dropdown) has a preview field and a down arrow, and when clicked opens a list of options.

> Example: Font select dropdown.
For more information, see [Split Button]({{site.baseurl}}../component/split).

### Menu Button

A toolbar menu button is a toolbar button that opens a menu on click, which can also contain submenu. This is useful if you want to group actions together that would otherwise be several buttons on the toolbar, or if you don't want a toolbar and a menubar since this allows you to pull menus into the toolbar.

> Example: the table plugin's table toolbar button, which opens a menu very similar to table's menubar menu, or its context menu.
For more information, see [Menu Button]({{site.baseurl}}../component/menu).

## How to Create Custom Toolbar Buttons

The methods for adding custom toolbar buttons are in the UI Registry part of the editor API `editor.ui.registry`. The API has four methods for adding toolbar buttons, one for each type of toolbar button:

* `editor.ui.registry.addButton`(identifier, configuration)
* `editor.ui.registry.addToggleButton`(identifier, configuration)
* `editor.ui.registry.addSplitButton`(identifier, configuration)
* `editor.ui.registry.addMenuButton`(identifier, configuration)

The two arguments these methods take are:

* `identifier` - a unique name for the button
* `configuration` - an object containing your configuration for that button. 

> Note: Although there are some common configuration options, each type of button has custom options. We recommend reading the relevant page for the type of button you're creating.

To actually add a custom toolbar button to the editor, you need to define it within the `setup` callback of your TinyMCE configuration. This callback is automatically invoked for every initialised editor instance. It receives a reference to the editor instance as its argument, which we use to access the UI Registry API. 

### Example of adding a basic button that triggers an alert when clicked:

```js
tinymce.init({
  selector: '#editor',
  toolbar: 'myCustomToolbarButton',
  setup: (editor) => {
    editor.ui.registry.addButton('myCustomToolbarButton', {
      text: 'My Custom Button',
      onAction: () => alert('Button clicked!')
    });
  }
});
```
> Note: The identifier used to create the basic button is included in the `toolbar` option of our TinyMCE configuration. Without this, our button won't be added to the toolbar.




