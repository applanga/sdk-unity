# Applanga SDK for Unity
***
*Version:* 1.0.38

*URL:* <https://www.applanga.com> 
***

## Installation
1.  Download and import the ***[Applanga.unitypackage](https://github.com/applanga/sdk-unity/raw/master/Applanga.unitypackage)***. A new menu item labeled **Applanga** will appear in the editor.
2.  You can always get the latest version by clicking ***Applanga -> Update SDK***.

## Configuration
1. Download the *Applanga Settings File* for your project from the Applanga app overview in the dashboard by clicking the ***[Prepare Release]*** button and then clicking ***[Get Settings File]***. 
2. Add the *Applanga Settings File* to your ***Resources*** folder. The file extension will be automatically changed to *'.applanga.bytes'*. This will happen when adding the file as an asset or when executing the next step.
3. Select ***Applanga -> Initialize -> For Sqlite*** to use the default Sqlite database implementation or ***Applanga -> Initialize -> For In-Memory DB*** to use an in-memory database implementation and the Applanga object will be added to your scene. This should be done at least on the first scene that your game loads. The Applanga object is set to not be destroyed on scene change.
3. Now, if you start your game you should see a log message that confirms that Applanga was initialized or a warning in case of a missing settings file.


## Usage

### Basic:

- **UI:** Select ***Applanga -> AutoTranslate Scene*** to attach the Applanga AutoTranslate Component to all Objects with a UI.Text Component and all TextMeshes in the current openend scene and to autogenerate Applanga ID's for them.
All GameObjects that have the AutoTranslate Component attached get translated when they get [Awake](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html) with the current cached translation state and whenever the Applanga SDK retrieves new updated translations. *(see section **5. Automated UI Localization** for more details)* 

- **Scripts:** Use the following code to retrieve a localized string programmatically. *(see section **4. Script Localization** for more details)
  
  ```csharp
  Applanga.GetString("APPLANGA_ID", "DEFAULT_VALUE")
  ``` 

- **Synchronization:** When you start a scene that includes the Applanga Object it initializes on [Awake](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html) and  synchronizes the local string data with the Applanga dashboard.
If you press play from within the Editor, built your game as a Development Build or if *Draft Mode* is activated then all texts that you supply to Applanga.GetString and AutoTranslate(able) Components will also be uploaded to the dashboard after they are activated and if the IDs do not yet exist or if they have empty values. 

### Extended:

1. To get notified after the localization updates completes (e.g. to show a LoadingScreen at beginning of your App) set a callback event on the ``First Update Callback Event`` of the Applanga gameobject.  The event function should take a bool as parameter, which indicates if the update was successful.

	```csharp
	// example event function
	public void ApplangaCallbackDelegate (bool success) {
			...
	}
	```
	
2. The **Settings** field allows you to specify various optional settings as name/value pairs *(see section **Optional settings**)*.
3. The **Editor Draft Mode** checkbox allows you to directly activate or deactivate the [Draft Mode](https://applanga.com/docs#draft_on_device_testing). It will be ignored outside of the editor.
4. To use Applanga in a WebGL project the **Use Memory DB** checkbox wich allows you to switch to an In-memory DB implementation. Please see **In-memory Database** under **Optional Settings** for more Information.
5. If you plan to deploy to the **WebGL** platform, please see **In-memory Database** under **Optional Settings** for more Information. 

6. **Script Localization**
 
    To load a string for a specific ID in the current language, use the functions described in this section. Note that if the ID you requested does not exist, the default value will be returned and the string may be created in the dashboard. 
 	
   6.1 **Setup**
   
   ```csharp
   using ApplangaSDK;
   using ApplangaSDK.Unity;
   ```
   Should be added to any script that needs to call Applanga methods.
 	
   6.2  **Strings**
   
	```csharp
	// get a translated string for the current device locale
	Applanga.GetString("APPLANGA_ID", "DEFAULT_VALUE");
	```
	
   6.3 **Arguments**
       
	```csharp
	// get a translated string with formatted arguments
	// using the default c# string format parameters {0}, {1}, {2} etc.
	// @see https://msdn.microsoft.com/en-us/library/system.string.format(v=vs.110).aspx
	Applanga.GetString("APPLANGA_ID", "DEFAULT_VALUE", "arg1", "arg2", "arg3");        
	```
   
   6.4 **Named Arguments**
   
	```csharp             
	// if you pass a Dictionary<string, string> you can get a translated string
	// with named arguments being inserted. %{someArg} %{anotherArg} etc.
	Dictionary<string, string> arg = new Dictionary<string, string>()
	args.Add("someArg","awesome");
	args.Add("anotherArg","crazy");
	Applanga.GetString("APPLANGA_ID", "DEFAULT_VALUE", args);
	```
        
   Example:
    
     *APPLANGA_ID* = *"This value of the argument called someArg is **%{someArg}** and the value of anotherArg is **%{anotherArg}**. You can reuse arguments multiple times in your text, which is **%{someArg}**, **%{anotherArg}** and **%{someArg}.**"*	
    
   gets converted to:
   
    *"The value of the argument called someArg is awesome and the value of anotherArg is crazy. You can reuse arguments multiple times in your text, which is awesome, crazy and awesome."*    
        
   6.5 **Pluralization**
		
	```csharp 
	// get a string in the given quantity
	Applanga.GetString("APPLANGA_ID", "DEFAULT_VALUE", quantity);
	```
		
	Available pluralization rules:

	```csharp 	
	Zero,
	One,
	Two,
	Few,
	Many,
	Other
	```
	
	You specify the quantity (int) as the last parameter and Applanga will pick the best pluralization rule based on: [http://unicode.org/.../language_plural_rules.html	](http://www.unicode.org/cldr/charts/latest/supplemental/language_plural_rules.html)
		
	In the dashboard you create a **pluralized ID** by appending the Pluralization rule to your **ID** in the following format: `[zero]`, `[one]`,`[two]`,`[few]`,`[many]`, `[other]`.
	
	So the ***zero*** pluralized ID for ***"APPLANGA_ID"*** is ***"APPLANGA_ID[zero]"***.
	
	If uploading strings is enabled and you call Applanga.GetString() with a quantity, Applanga will create the corresponding pluralized ID for the supplied default value.
               
7. **Automated UI Localization**
	
	You can add the *AutoTranslate* script to any UI.Text component or TextMesh component to have the text automatically translated on [Awake](https://docs.unity3d.com/ScriptReference/MonoBehaviour.Awake.html). 
	
	If you want to localize all supported objects in the scene you can click **Applanga -> AutoTranslate Scene** and *AutoTranslate* components will be attached to all supported text objects. All *AutoTranslate* components will update their text values after a successful update call or a successful language change.
	
	If you do not want to use the automatically generated IDs you can override them in the AutoTranslate component.
	
	***Note: On Input Fields, *AutoTranslate* components will only be attached to the placeholder Text component and the Input Field itself will not be tranalated.***
	
	To only translate a single object or a prefab click **Applanga**->**AutoTranslate selected**. This will add the *AutoTranslate* component to that object and generate an Applanga_ID based on the scene name and the objects hierarchy. 

8. **Update Content**
 
	To trigger an update call:
	
	```csharp
	Applanga.Update (  new ApplangaCallbackDelegate((bool success) => {
			//enter code to be called when update is complete   
	}));
	```
	
    This will request the base language along with the long (e.g. "en_US") and short (e.g. "en") versions of the device's current language.
    If you are using groups, be aware that this will only update the **main** group.
    	
    To trigger an update for a specific set of groups (see [groups](https://applanga.com/docs#groups)) and languages call:
    
	```csharp
	List<string> groups = new List<string>();
	groups.Add("GroupA");
	groups.Add("GroupB");
	List<string> languages = new List<string>();
	languages.Add("en");
	languages.Add("de");
	languages.Add("fr_CA");

	Applanga.Update(groups, languages, new ApplangaCallbackDelegate((bool success) => {
			//enter code to be called when update is complete    
	}));
	```
	
9. **Change Language**
  
  	You can change your app's language at runtime using the following call: 
  	
	```csharp
	bool success = Applanga.SetLanguage(language);
  	```
  	 
  	 *language* must be the iso string of a language that has been added in 	the dashboard. It does not have to correspond to any Unity system language.
  	The return value will be *true* if the language could be set or if it already was the 	current language, otherwise it will be *false*.   	The newly set language will be saved. 
  	To reset it back to the device language call:
  	
  	```csharp
	Applanga.SetLanguage(null);
  	```	
  		
  	The *language* parameter is expected in the format **[language]-[region]** or 	**[language]_[region]** with the region being optional. Examples: "fr_CA", "en-us", "de". 
  	
  	If you have problems switching to a specific language you can update your settings file 	or specifically request that language within an update content call *(see section **7. Update Content**)*. You can also 	specify the language as a default language to have it requested on each update call *(see section **Optional settings**)*.

10. **Draft Mode** To activate draft mode (see the dashboard docu on [Draft Mode](https://applanga.com/docs#draft_on_device_testing)) on any touch devices you have to hold four fingers down on the screen for four seconds and enter the draft mode key in the Dialog. In the Editor you can tick or untick the ``Editor Draft Mode`` check box on the Applanga object to activate or deactivate the draft mode directly, this will only have an effect inside the editor.

11. **Screenshots for Translation Context** The Applanga SDK offers the functionality to upload screenshots of your app, while collecting meta data such as the current language, resolution and the Applanga translated strings that are visible, 	including their positions.
 	Each screenshot will be assigned to a tag. A tag may have multiple screenshots with differing core meta data: language, app version, device, plattform, OS and resolution. 
 	
 	You can read more here: [Manage Tags](https://applanga.com/docs#manage_tags) and here: [Uploading screenshots](https://applanga.com/docs#uploading_screenshots).
 	
 	11.1 **Make screenshots manually**
 	
 	To manually make a screenshot you first have to set your app into [draft mode](https://applanga.com/docs#draft_on_device_testing).
 	 
 	With your app in draft mode, all you have to do is to make a two finger swipe downwards.
 	This will show the screenshot menu and load a list of [tags](https://applanga.com/docs#manage_tags).
 	
 	You can now choose a tag and press *capture screenshot* to capture and upload a screenshot including all meta data for the currently visible screen and assign it to the selected tag.
 	Tags have to be created in the dashboard before they are available in the screenshot menu.
 	
 	11.2 **Display screenshot menu programmatically**
 	
 	You have the option to open the screenshot menu programmatically, this also requires the app to be in draft mode:
 		
 	```csharp
	Applanga.SetScreenshotMenuVisible (true);
  	```	
 				
 	11.3 **Make screenshots programmatically**
 	
 	To create a screenshot programmatically you call the following function:
 	
 	```csharp
	List<string> applangaIDs = new List<string>{"Start","Settings","Quit"};
	Applanga.CaptureScreenshot("MainMenu", applangaIDs);
	```
			
 	The Applanga SDK tries to find all IDs on the screen but you can pass additional IDs in the **applangaIDs** parameter. 


## Optional settings


**Default groups and languages**

You can specify a set of default groups and languages on the Applanga object, which will be updated on every Applanga.update() or Applanga.updateGroups() call. These groups and languages will be added in addition to values that you specifiy by code.
	

1. **Specify default groups**
Click on **Settings** on the Applanga object and enter **1** or **2** in the **Size** field, depending on if you intend to add groups and languages or only groups.
Enter **ApplangaUpdateGroups** into the **Name** field and a comma seperated list of groups into the **Value** field (e.G., *"GroupA, GroupB"*).
	
2. **Specify default languages**
Click on **Settings** on the Applanga object and enter **1** or **2** in the **Size** field, depending on if you intend to add groups and languages or only languages.
Enter **ApplangaUpdateLanguages** into the **Name** field and a comma seperated list of languages corresponding to the applanga dashboard language isos, into the **Value** field (e.G., *"fr, de_AT"*).

**Screenshot Menu Hotkeys**

You also have the possibility to set a number of keys as a Hotkey combination to activate the screenshot menu (requires the draft mode to be active). Select the Applanga gameobject then find **Screenshot Menu Activation Keys**. Here you can choose the number of Keys you want to use and pick the actual Keys you want to use. The screenshot menu will then be toggled at Runtime if all keys are pressed simultaneously and the draft mode is active.

**In-memory Database**

You have the option to use an In-memory Database by checking the checkbox *Use Memory DB* on the Applanga gameobject. Or by using ***Applanga -> Initialize -> For In-Memory DB***. 
This Database variant will load all Data for used languages into memory and only persist them after successful updates.
It will automatically be used if you build for the *WebGL* platform, due to platform retsrictions.

***Note:*** For the memory DB to load the initial data from the settingsfile, it's necessary to convert the data: click ***Applanga -> Initialize -> For In-Memory DB***. This is required when deploying for *WebGL* or activating the *Use Memory DB* option. It will also remove Sqlite library dependencies.

If you want to deploy for another platform and use Sqlite you have to execute ***Applanga -> Initialize -> For Sqlite***.


## Unity Language mapping

Applanga detects the system language using Application.systemLanguage and maps it to Applanga Iso strings following this table:

* SystemLanguage.Afrikaans -> **af**
* SystemLanguage.Arabic -> **ar**
* SystemLanguage.Basque -> **eu**
* SystemLanguage.Belarusian -> **be**
* SystemLanguage.Bulgarian -> **bg**
* SystemLanguage.Catalan -> **ca**
* SystemLanguage.Chinese -> **zh**
* SystemLanguage.ChineseSimplified -> **zh-Hans**
* SystemLanguage.ChineseTraditional -> **zh-Hant**
* SystemLanguage.Czech -> **cs**
* SystemLanguage.Danish -> **da**
* SystemLanguage.Dutch -> **nl**
* SystemLanguage.English -> **en**
* SystemLanguage.Estonian -> **et**
* SystemLanguage.Faroese -> **fo**
* SystemLanguage.Finnish -> **fi**
* SystemLanguage.French -> **fr**
* SystemLanguage.German -> **de**
* SystemLanguage.Greek -> **el**
* SystemLanguage.Hebrew -> **he**
* SystemLanguage.Hungarian -> **hu**
* SystemLanguage.Icelandic -> **is**
* SystemLanguage.Indonesian -> **id**
* SystemLanguage.Italian -> **it**
* SystemLanguage.Japanese -> **ja**
* SystemLanguage.Korean -> **ko**
* SystemLanguage.Latvian -> **lv**
* SystemLanguage.Lithuanian -> **lt**
* SystemLanguage.Norwegian -> **no**
* SystemLanguage.Polish -> **pl**
* SystemLanguage.Portuguese -> **pt**
* SystemLanguage.Romanian -> **ro**
* SystemLanguage.Russian -> **ru**
* SystemLanguage.SerboCroatian -> **sr**
* SystemLanguage.Slovak -> **sk**
* SystemLanguage.Slovenian -> **sl**
* SystemLanguage.Spanish -> **es**
* SystemLanguage.Swedish -> **sv**
* SystemLanguage.Thai -> **th**
* SystemLanguage.Turkish -> **tr**
* SystemLanguage.Ukrainian -> **uk**
* SystemLanguage.Vietnamese -> **vi**
