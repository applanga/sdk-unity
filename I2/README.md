# Applanga SDK I2 Localization Bridge
***

Applanga can be configured to co-exist with the I2 Localization package.
The benefits are to use, manage and store all your strings in the Applanga Dashboard instead of local files or Google Sheets.
After installation and configuration all existing strings will be uploaded to the Applanga Dashboard and the Applanga Dashboard will become the main translation POT and will update local strings in the editor and always on start of your game.
You can add new strings inside the I2 interface but if you want to edit them you should head over to the Applanga Dashboard
## Installation
1.  Download and import the ***[Applanga.unitypackage](https://github.com/applanga/sdk-unity/raw/master/Applanga.unitypackage)***. A new menu item labeled **Applanga** will appear in the editor.
2.  You can always get the latest version by clicking ***Applanga -> Update SDK***.
3. Download and import the ***[I2Applanga.unitypackage](https://github.com/applanga/sdk-unity/raw/master/I2/I2Applanga.unityPackage)***.

## Configuration
1. Download the *Applanga Settings File* for your project from the Applanga app overview in the dashboard by clicking the ***[Prepare Release]*** button and then clicking ***[Get Settings File]***. 
2. Add the *Applanga Settings File* to your ***Resources*** folder. The file extension will be automatically changed to *'.applanga.bytes'*. This will happen when adding the file as an asset or when executing the next step.
3. Select ***Applanga -> Initialize -> For I2Localization*** to use the default Sqlite database implementation combined with I2 Localization 
4. Now, if you start your game you should see a log message that confirms that Applanga was initialized or a warning in case of a missing settings file.
5. If you are using I2 with Google Sheets with i2 make sure to set the **Auto Update Frequency** to **Never** since the strings should and will be updated from Applanga and not from Google.

## Usage

Please Refer to the I2 Documentation on how to use I2 and the [Applanga Documentation and Chat](https://applanga.com/#!/docs) on how to use Applanga