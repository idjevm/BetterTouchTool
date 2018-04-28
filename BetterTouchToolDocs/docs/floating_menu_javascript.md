# Triggering Scripting Functions from the Floating Web View

This is a very recent feature which is only available in **versions greater than 2.460**. 

The Floating Web View allows you to trigger various scripting functions via Java Script.

The available scripting interfaces are:
* trigger_named
* update_touch_bar_widget
* trigger_action
* execute_assigned_actions_for_trigger
* refresh_widget
* update_trigger
* add_new_trigger 
* delete_trigger


## Available Scripting Interfaces

BetterTouchTool automatically injects the BTT Object in any HTML you provide to the Floating Web View. This object has one method called "callHandler".

```window.BTT.callHandler()``` accepts three parameters (only the first is required).
1. the name of the scripting interface you want to trigger. This is a string.
2. Any additional config needed. This is a normal Java Script object
3. A callback function which will be called with the result of the call (if any). function(result) {}

### **trigger_named**
This method will trigger the specified named trigger (which can be configured in the "Other" tab in BetterTouchTool.)


#### Example:
```JavaScript
 window.BTT.callHandler('trigger_named', {trigger_name: 'Action5'})
```
---



### **update_touch_bar_widget**
This method will update the contents of a Touch  Bar Script Widget (identified by its uuid). You can provide a new text to show, a new icon and a new background color.

For the icon you can either provide it directly using the icon_data parameter (must be base64 encoded) or you can provide a file path (via the icon_path parameter) that points to the new icon.

You can get the uuid by right-clicking any script widget in BTT.

#### Example:
```JavaScript

var theActionConfig= {
	text: "hi there!",
	icon_path: "/Users/andi/Desktop/test.png",
	background_color: "200,100,100,255"	
};


window.BTT.callHandler('trigger_named', {uuid: '9990CE09-9820-4D67-9C52-8BABAB263056', 'json': JSON.stringify(theActionConfig)})
```
---


### **trigger_action**
This method will trigger any of BetterTouchTool's predefined actions (or any combination of them).

You need to provide a JSON description of the action you want to trigger. The easiest way to get such a JSON description is to right-click the trigger you have configured in BetterTouchTool and choose "Copy JSON". This will copy the complete JSON (including the configuration for the trigger itself), but this action will ignore anything that's not needed. (or you can delete the not needed parts)
#### Example:
```JavaScript
var actionDefinition = {
  "BTTPredefinedActionType" : 153, 
  "BTTPredefinedActionName" : "Move Mouse To Position", 
  "BTTMoveMouseToPosition" : "{100, 100}", 
  "BTTMoveMouseRelative" : "6"
};

window.BTT.callHandler('trigger_action', {json: JSON.stringify(actionDefinition)})
```

---


### **execute_assigned_actions_for_trigger**
This method execute all the assigned actions for a given trigger (i.e. gesture, shortcut, drawing etc.) identified by its uuid.

You can get the uuid by right-clicking any configured trigger in BetterTouchTool.

#### Example
```JavaScript
window.BTT.callHandler('execute_assigned_actions_for_trigger', {uuid: '2F34005D-4537-464D-94E9-A7F42DA39DF1'})
```

---


### **refresh_widget**
This method will execute all scripts assigned to a script widget and update its contents accordingly.

The widget is identified by its uuid, which you can get by right-clicking the widget in BetterTouchTool.

#### Example
```JavaScript

window.BTT.callHandler('refresh_widget', {uuid: '2F34005D-4537-464D-94E9-A7F42DA39DF1'})
```

---


### **update_trigger**
This method will update the configuration of any trigger you have configured in BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide the uuid of the trigger you want to update (get by right-clicking it in BTT) and a JSON object defining the updates. To know how the JSON object should look like, right-click the trigger in BTT and choose "Copy JSON".

#### Example:
Hint: don't forget to use JSON.stringify() before passing the updateDefinition object.

```JavaScript
var updateDefinition = {
	"BTTTouchBarButtonName" : "New Name",
	"BTTTouchBarItemIconHeight" : 25
}

window.BTT.callHandler('update_trigger', {json: JSON.stringify(updateDefinition)})
```

---


### **add_new_trigger**
This method will add a new trigger to BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide a JSON object defining the new trigger. To know how the JSON object should look like, right-click any existing trigger in BTT and choose "Copy JSON".

#### Example
```JavaScript
var newTriggerDefinition = {
  "BTTTriggerClass" : "BTTTriggerTypeKeyboardShortcut",
  "BTTPredefinedActionType" : 5,
  "BTTPredefinedActionName" : "Mission Control",
  "BTTAdditionalConfiguration" : "1179648",
  "BTTTriggerOnDown" : 1,
  "BTTEnabled" : 1,
  "BTTShortcutKeyCode" : 2,
  "BTTShortcutModifierKeys" : 1179648,
  "BTTOrder" : 3
}

window.BTT.callHandler('add_new_trigger', {json: JSON.stringify(newTriggerDefinition)})
```


### **delete_trigger**
This method will delete a trigger from BetterTouchTool.
You need to provide the uuid of the trigger you want to delete (get by right-clicking it in BTT).

#### Example
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

window.BTT.callHandler('delete_trigger', {uuid: '2F34005D-4537-464D-94E9-A7F42DA39DF1'})

```

---

