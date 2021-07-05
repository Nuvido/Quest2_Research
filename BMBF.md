# BMBF

## ANDROID MANIFEST

## CODE

### BMBF.dll
BMBF.dll contains the Main activity, logging tools, feed config
- [Constants](SystemUX_Intents)

#### Main Activity
Main activity first begins with importing varies system and custom libaries. The application then begins to create a web view instance, and then checks whether it has write permissions.  The webview instance uses the following settings.
##### User Agent
- Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2049.0 Safari/537.36 BMBF_Quest/ 
##### Miscellaneous
- JavaScriptEnabled = true;
- AllowContentAccess = true;
- CacheMode = -1;
- Focusable = true;
- MediaPlaybackRequiresUserGesture = false;
- DomStorageEnabled = true;
- DatabaseEnabled = true;
- Database path: /data/data/" + this._browserView.Context.PackageName + "/databases/"

The application will then excute the following events.
- Display Browser
- Check if BMBF Has Write Access
- Kill the beatsaber application, if its running.
#### User Server
When a user intitiate a user server the following code is executed.
- Application will look for wireless interfaces, then if there is none intitiates the server on 127.0.0.1, if one is found it will use the corresponding IP.
- Starts a server on the ip, and a specific port.
- User will go on the web server and is displayed with an index.html file. 
- All users requests and interactions will be handled by the application
#### BMBF Service
BMBF service is repsonsible for getting/making a cache file containg various service logs.
#### Beat Saber Modder
- Copies original beatsaber apk to a temporary location
- Prompts user to uninstall old beat saber application
- In some cases will backup user data from the location /sdcard/Android/data/com.beatgames.beatsaber/files/PlayerData.dat to /sdcard/BMBFData/Backups/
- Checks whether the following files exist. beatsaber-unmodded.apk, beatsaber-modded-donotuse.apk, 
- Checks whether Temp APK has specific headers. 
- Adds custom libmodloader.so & libmain.so & libunity.so & libBMBFmod.so
- Signs apk with a [Private Key](SystemUX_Intents)

