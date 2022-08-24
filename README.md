# Unity-JSON-Settings-System
Extendable settings system for Unity UI. Data saved through JSON serialization.

# Structure: 
SettingsSystem is a MonoBehavior object that will hold your Settings object and serialize it into JSON. Create another script of your choosing that will define 2 of its static variables.
 1. path: where your data will be stored
 2. defaultSettings: the default version of the settings object.

A Settings object contains a list of SettingsCatagory objects in its sole property 'catagories'. This object is designed to hold all the settings for your project. To access data, objects can freely access the public 'settings' property of SettingsSystem, which contains a version of your current settings. To be notified of changes in settings, objects can subscribe to the onSettingsChanged event of SettingsSystem.

A SettingsCatagory object defines a subset of settings - eg. audio, display. It countains a list of SettingsProperty inside the property 'properties'. It also contains a string 'name' which denotes its name.

A SettingsProperty object is an abstract class that defines a editable settings property, eg. a float, a bool etc. It contains a string name and a string tag. Tags are useful when linking properties to prefabs when you generate your settings UI. You can extend SettingsProperty to make your own editable properties. Currently only 3 extensions of it exist in this package: SettingsFloatProperty, SettingsBoolProperty and SettingsHeaderProperty.

SettingsViewer is a Unity MonoBehavior object that you attach to a canvas you want to hold your settings display. It will parse and generate UI that can edit your settings. It should contain 2 scroll views, one to select a SettingsCatagory and another to display its various SettingsProperty. It has a few SerializedFields to define.
1. Page Parent: the content part of the scroll view for SettingsProperty.
2. Catagory Button Parent: the content part of the scroll view for SettingsCatagory.
3. Settings System: reference to this scene's SettingsSystem
4. Catagory Button Prefab: reference to a prefab of a selectable button used to select SettingsProperty.
5. Property Objects: reference to a list of prefabs used to represent SettingsCatagory.

The CatagoryButtonPrefab must contain the SettingsCatagorySelectButton script. Add the relevant button and text UI properties of the prefab button to the script in the editor.

Each SettingsProperty extension has a corresponding prefab of that extends SettingsPropertyObject. SettingsPropertyObject will give the prefab access to the SettingsProperty (in the settingsProperty field) object it represents. The object will have to cast that down to its specific SettingsProperty child class and is responsible for displaying and allowing the property to be edited. Whenever an edit occurs, it should call the provided (saveSettings) function.

To get a better understanding of how this structure works, check out the example scene.

To set up using the package, it is recommended that you copy the working example in the example scene and make relevant changes to suit your needs.


