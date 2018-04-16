# Integrated Webserver

This is a very recent feature which is only available in **versions greater than 2.430**. 

BetterTouchTool has a basic integrated Webserver. It is **disabled** by default and can be activated in the advanced preferences.

![webserver](media/webserver.png)

The integrated webserver can be used for a few very interesting usecases:

* **In combination with the predefined action "Show Floating WebView/HTML Menu"** (This allows you to create completely customizable popup menus). See  [Floating HTML Menu](floating_html_menu.md)
* To easily trigger BetterTouchTool actions from websites (e.g. when building a custom "Dashboard" thingy)
* Controlling your computer from tablet's or smartphone's via custom dashboards


# Basic settings
The webserver settings are all located in the advanced preferences. There are not many settings.

* You can choose a port (on first start it will automatically assign some random port if you don't enter any) 
* You can set a shared secret (which you should if you make it available in your network). This shared secret must then be included in all urls to the server (e.g. https://127.0.0.1:12345/?shared_secret=v3rY_$ecre7)
* You can choose on which interface the server should listen. The default is 127.0.0.1 (which means only applications on your computer can access it). If you want to make it available in your network, you need to enter your computers local IP (can be found in System Preferences => Network.)
* You can enable HTTPS. This will use the BetterTouchToolRemote_New certificate in your keychain. You need to make this a trusted certificate, otherwise your browsers will complain (on macOS you can do it by going to your keychain, right-clicking it => get info => trust => always trust)

If you want the server to serve files, you can put them in this directory (doesn't exist by default):
~/Library/Application Support/BetterTouchTool/BTTWebServer/


## Methods that can be triggered using the webserver.

### **trigger_named**
This method will trigger the specified named trigger (which can be configured in the "Other" tab in BetterTouchTool.)

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/trigger_named/?trigger_name=TriggerName"
```

### **update_touch_bar_widget**
This method will update the contents of a Touch  Bar Script Widget (identified by its uuid). You can provide a new text to show, a new icon and a new background color.

For the icon you can either provide it directly using the icon_data parameter (must be base64 encoded) or you can provide a file path that points to the new icon (via the icon_path parameter).

You can get the uuid by right-clicking any script widget in BTT.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/update_touch_bar_widget/?uuid=CC46E199-B07D-4BF7-AC36-48AAE558540B&text=updatedText&icon_path=/Users/andi/Desktop/test.png&background_color=200,200,100,255"

```

---


### **trigger_action**
This method will trigger any of BetterTouchTool's predefined actions (or any combination of them).

You need to provide a JSON description of the action you want to trigger. The easiest way to get such a JSON description is to right-click the trigger you have configured in BetterTouchTool and choose "Copy JSON". This will copy the complete JSON (including the configuration for the trigger itself), but this action will ignore anything that's not needed. (or you can delete the not needed parts)
#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/trigger_action/?json={ \"BTTPredefinedActionType\" : 153, \"BTTPredefinedActionName\" : \"Move Mouse To Position\", \"BTTMoveMouseToPosition\" : \"{100, 10}\", \"BTTMoveMouseRelative\" : \"6\" }"
```
---


### **execute_assigned_actions_for_trigger**
This method execute all the assigned actions for a given trigger (i.e. gesture, shortcut, drawing etc.) identified by its uuid.

You can get the uuid by right-clicking any configured trigger in BetterTouchTool.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/execute_assigned_actions_for_trigger/?uuid=C40D3AE2-2F4E-49B1-A00C-F7E4C3632F07" 

```


---


### **refresh_widget**
This method will execute all scripts assigned to a script widget and update its contents accordingly.

The widget is identified by its uuid, which you can get by right-clicking the widget in BetterTouchTool.

#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/refresh_widget/?uuid=C40D3AE2-2F4E-49B1-A00C-F7E4C3632F07" 

```

---


### **update_trigger**
This method will update the configuration of any trigger you have configured in BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide the uuid of the trigger you want to update (get by right-clicking it in BTT) and a JSON object defining the updates. To know how the JSON object should look like, right-click the trigger in BTT and choose "Copy JSON".


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/update_trigger/?uuid=0E2F7963-E64C-403A-8591-C3725D4D9ADC&json={\"BTTTouchBarButtonName\" : \"New Name2\",  \"BTTTriggerConfig\" : {\"BTTTouchBarItemIconHeight\" : 30}}"
```

---


### **add_new_trigger**
This method will add a new trigger to BTT (i.e. gestures, shortcuts, touchbar items etc.).

You need to provide a JSON object defining the new trigger. To know how the JSON object should look like, right-click any existing trigger in BTT and choose "Copy JSON".


#### Example Terminal Command (but you can call the URL however you like)
```Bash
open "http://127.0.0.1:12345/add_new_trigger/?json={ \"BTTTriggerClass\" : \"BTTTriggerTypeKeyboardShortcut\", \"BTTPredefinedActionType\" : 5, \"BTTPredefinedActionName\" : \"Mission Control\", \"BTTAdditionalConfiguration\" : \"1179658\", \"BTTTriggerOnDown\" : 1, \"BTTEnabled\" : 1, \"BTTShortcutKeyCode\" : 2, \"BTTShortcutModifierKeys\" : 1179648, \"BTTOrder\" : 3 }"
```





