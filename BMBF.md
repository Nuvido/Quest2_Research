# BMBF

## ANDROID MANIFEST

## CODE

### BMBF.dll
BMBF.dll contains the Main activity, logging tools, feed config

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
