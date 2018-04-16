# Scripting BetterTouchTool using Apple Script

This is a very recent feature which is only available in **versions greater than 2.430**. 

BetterTouchTool has a small but powerful Apple Script interface which will be described here.

The available scripting interfaces are:
* trigger_named
* update_touch_bar_widget
* trigger_action
* execute_assigned_actions_for_trigger
* refresh_widget
* update_trigger
* add_new_trigger 

## Available Scripting Interfaces

### **trigger_named**
This method will trigger the specified named trigger (which can be configured in the "Other" tab in BetterTouchTool.)

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

trigger_named "TriggerName" 

end tell
```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.trigger_named("TriggerName");
```
---



### **update_touch_bar_widget**
This method will update the contents of a Touch  Bar Script Widget (identified by its uuid). You can provide a new text to show, a new icon and a new background color.

For the icon you can either provide it directly using the icon_data parameter (must be base64 encoded) or you can provide a file path (via the icon_path parameter) that points to the new icon.

You can get the uuid by right-clicking any script widget in BTT.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

update_touch_bar_widget "9990CE09-9820-4D67-9C52-8BABAB263056" text "newButtonText" icon_path "~/Desktop/005-ShoppingBasket@2x.png" background_color "255,100,100,255"

end tell
```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.update_touch_bar_widget("9990CE09-9820-4D67-9C52-8BABAB263056", 
{
	text: "hi there!",
	icon_path: "/Users/andi/Desktop/test.png",
	background_color: "200,100,100,255"	
});
```
---


### **trigger_action**
This method will trigger any of BetterTouchTool's predefined actions (or any combination of them).

You need to provide a JSON description of the action you want to trigger. The easiest way to get such a JSON description is to right-click the trigger you have configured in BetterTouchTool and choose "Copy JSON". This will copy the complete JSON (including the configuration for the trigger itself), but this action will ignore anything that's not needed. (or you can delete the not needed parts)
#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

	trigger_action "{\"BTTPredefinedActionType\":100}"

end tell

```
#### Java Script for Automation Example:
Hint: don't forget to use JSON.stringify() before passing the actionDefinition object.
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');
var actionDefinition = {
  "BTTPredefinedActionType" : 153, 
  "BTTPredefinedActionName" : "Move Mouse To Position", 
  "BTTMoveMouseToPosition" : "{10, 10}", 
  "BTTMoveMouseRelative" : "6"
};


BetterTouchTool.trigger_action(JSON.stringify(actionDefinition));

```

---


### **execute_assigned_actions_for_trigger**
This method execute all the assigned actions for a given trigger (i.e. gesture, shortcut, drawing etc.) identified by its uuid.

You can get the uuid by right-clicking any configured trigger in BetterTouchTool.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"
	execute_assigned_actions_for_trigger "2F34005D-4537-464D-94E9-A7F42DA39DF1"
end tell

```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.execute_assigned_actions_for_trigger("2F34005D-4537-464D-94E9-A7F42DA39DF1");

```

---


### **refresh_widget**
This method will execute all scripts assigned to a script widget and update its contents accordingly.

The widget is identified by its uuid, which you can get by right-clicking the widget in BetterTouchTool.

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"
	refresh_widget "2F34005D-4537-464D-94E9-A7F42DA39DF1"
end tell

```
#### Java Script for Automation Example:
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');

BetterTouchTool.refresh_widget("2F34005D-4537-464D-94E9-A7F42DA39DF1");

```

---


### **update_trigger**
This method will update the configuration of any trigger you have configured in BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide the uuid of the trigger you want to update (get by right-clicking it in BTT) and a JSON object defining the updates. To know how the JSON object should look like, right-click the trigger in BTT and choose "Copy JSON".

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

update_trigger "2F34005D-4537-464D-94E9-A7F42DA39DF1" json "{\"BTTTouchBarButtonName\" : \"New Name\",  \"BTTTouchBarItemIconHeight\" : 25}"

end tell


```
#### Java Script for Automation Example:
Hint: don't forget to use JSON.stringify() before passing the actionDefinition object.
```JavaScript
var BetterTouchTool = Application('BetterTouchTool');
var updateDefinition = {
	"BTTTouchBarButtonName" : "New Name",
	"BTTTouchBarItemIconHeight" : 25
}
BetterTouchTool.update_trigger("2F34005D-4537-464D-94E9-A7F42DA39DF1", {json: JSON.stringify(updateDefinition)});

```

---


### **add_new_trigger**
This method will add a new trigger to BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide a JSON object defining the new trigger. To know how the JSON object should look like, right-click any existing trigger in BTT and choose "Copy JSON".

#### Standard Apple Script Example:
```AppleScript
tell application "BetterTouchTool"

add_new_trigger "{ \"BTTTriggerClass\" : \"BTTTriggerTypeKeyboardShortcut\", \"BTTPredefinedActionType\" : 5, \"BTTPredefinedActionName\" : \"Mission Control\", \"BTTAdditionalConfiguration\" : \"1179658\", \"BTTTriggerOnDown\" : 1, \"BTTEnabled\" : 1, \"BTTShortcutKeyCode\" : 2, \"BTTShortcutModifierKeys\" : 1179648, \"BTTOrder\" : 3 }"

end tell

```
#### Java Script for Automation Example:
Hint: don't forget to use JSON.stringify() before passing the actionDefinition object.
```JavaScript

// this will add a new keyboard shortcut to BTT.
var BetterTouchTool = Application('BetterTouchTool');

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

BetterTouchTool.add_new_trigger(JSON.stringify(newTriggerDefinition))

```





