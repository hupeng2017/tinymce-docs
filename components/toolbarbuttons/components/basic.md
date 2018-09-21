---
layout: draft
title: Basic
title_nav: Basic
description: Basic Toolbar Button
keywords: basicmenu basic menu toolbarmenu
---

##BASIC BUTTON

### Config Options

| Name | Value | Requirement | Description |
|------| ------| ------------| ----------- |
| text | string | optional | text to display if no icon is found |
| icon | string | optional | CHECK HOW THIS WILL WORK REGARDING ICON PACKS |
| tooltip | string | optional | text for button tooltip  |
| disabled | boolean | optional| default: false - represents button state. is toggled by the button's api |
| onSetup | (api) => (api) => void | optional | default: () => () => {} - function that's invoked when the button is rendered. |
| onAction | (api) => void | required | function that's called when the button is clicked |
> Note:  See below for details on return type for onSetup and onAction.


### API

| Name | Value | Description |
|------| ------| ------------|
| isDisabled | ( ) => boolean | check if the button is disabled |
| setDisabled | (state: boolean) => void | set the button's disabled state |




### Explanation and Example

```js
tinymce.init({
 selector: '#editor',
 toolbar: 'customInsertButton customSelectiveInsertButton',
 setup: (editor) => {
  editor.ui.registry.addButton('customInsertButton', {
   text: 'My Button',
   onAction: (_) => editor.insertContent('&nbsp;<strong>It\'s my button!</strong>&nbsp;')
  });
​
  const toTimeHtml = (date) => `<time datetime="${date.toString()}">${date.toDateString()}</time>`;
​
  editor.ui.registry.addButton('customDateButton', {
   icon: 'insert-time',
   tooltip: 'Insert Current Date',
   disabled: true,
   onAction: (_) => editor.insertContent(toTimeHtml(new Date())),
   onSetup: (buttonApi) => {
    const editorEventCallback = (eventApi) => buttonApi.setDisabled(eventApi.element.nodeName.toLowerCase() === 'time');
    editor.on('NodeChange', editorEventCallback);
    return (buttonApi) => editor.off('NodeChange', editorEventCallback);
   }
  });
 }
});
```

This example adds two buttons to the toolbar. The first just inserts "It's my button!" into the editor when clicked.
​
The second button is an example of how onSetup works. This button inserts a `time` element containing the current date into the editor using a `toTimeHtml()` helper function - a simplified version of TinyMCE's [insertdatetime]({{site.baseurl}}/plugins/insertdatetime/) plugin.

Since it wouldn't make sense to insert a `time` element into another `time` element, we have used `onSetup` to listen to the editor's [`NodeChange` event]({{site.baseurl}}/advanced/events/#nodechange) and disable the button when the user's cursor is inside a `time` element (or "node"). We have also borrowed an icon from the `insertdatetime` plugin, and explicitly set `disabled` to `true` in the button configuration so that it is disabled when the button is created.

This probably isn't necessary, but is included as an example.

onSetup is a complex property. It requires a function that takes the button's API and returns a function that takes the button's API and returns nothing. That's because onSetup is run whenever its toolbar button is created, and the function it returns must be a callback for when the button is destroyed - essentially an `onTeardown` handler.

When you listen to events in `onSetup` using `editor.on(eventName, callback)`, you're binding a callback function to an event. Therefore, in the teardown handler you need to tell the editor which function to unbind from which event using `editor.off(eventName, callback)`.

> Note:

* The callback function is the same one you passed to `editor.on()`. In this case, because we're binding the `editorEventCallback` function to the `NodeChange` event when the button is created, we simply need to return `(api) => editor.off('NodeChange', editorEventCallback)`.
* If you don't listen to any editor events or only listen to the editor's `init` event, you can just return an empty function from onSetup - `return () => {};`.