# Working With Screens
## Navigating between screens

The `ScreenManager` class provides a screen stack you can use to push screen
Screens  can be popped automatically when user selects a **back button in the car screen** or uses the **hardware back button** available in some cars. 

```kotlin
screenManager.push(NextScreen())
```
##  Refresh the contents of a template

Your app can request the content of a `Screen` to be invalidated by calling the `Screen.invalidate()` method. 
The host subsequently calls back into your app’s `Screen.onGetTemplate()` method to retrieve the template with the new contents.