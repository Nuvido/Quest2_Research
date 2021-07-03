# Quest_Research
## Background Information
The oculus quest 2 is a HMD running the Snapdragon XR2. The device runs on a highly modified version of Android 10, running the 2020 September security patch.
## Glossary
Throughout this research, you may come across a few quest specific abbreviations or terms.
- OCMS (Oculus Media Services)
- NUX (New User Experience)
- GK (Gatekeeper)
- Telemetry (Tracking)
- Horizon (Social Services)
- Dogfood (In-House Beta)
## Quest Devices
1. Monterey (Quest)
2. Del Mar (Quest 2)
3. Seacliff (Unkown has eye tracking)

## App Signatures
Currently All system apps are signed via either one of the 3 Signatures.
1. Oculus Vr LLC
2. Security@oculus.com (Used in various system applications)
3. Facebook Technologies LLC (Only used in enterprise specific applications)


## Network Config
Clear text is not premitted if any of the urls contain the following, you should be able to change this by changing the net config file found in all system apps.
- fbcdn.net
- fbsbx.com
- facebookcorewwwi.onion
- fbcdn23dssr3jqnq.onion
- fbsbx2q4mvcl63pw.onion
- instagram.com
- cdninstagram.com
- workplace.com
- oculus.com
- facebookvirtualassistant.com
- discoverapp.com
- freebasics.com
- internet.org
        
## System Applications
The Quest 2 Operating system has a plethora of system applications all that have their purpose, here are the following system applications and a summary of what they do.
### Unified Telemetry
Unified Telemetry is used for Device Analytics, the device will send analytical data consisting of key information the following is what is sent in an average Telemetry event.
- BOOT REASON, LAST BOOT TIME,
- APP CRASH
- AUDIO COLLECTOR
- BATTERY SNAPSHOT
- SCREEN STATUS
- IS TRUSTED USER
- FILE OPERATIONS
- OS EXACT SIZE 
- APPLICATION SIZE (DALVIK)
- BATTERY SERIAL NUMBER
- BATTERY CAPACITY, RESISTANCE, CURRENT PERCENT, TEMP, CURRENT VOLTAGE, CHARGING STATUS, BATTERY HEALTH, BATTERY UPTIME (/sys/kernel/debug/wakeup_sources)
- SCREEN EVENTS (NOT YET IMPLEMENTED)
- NETWORK TYPE, ENCRYPTION, SSID, NETWORK FREQUENCY, QUALITY OF NETWORK, DECIBELS, IS NETWORK BLACKLISTED, WIFI CAPABILLITYS CHECK, INTERNET SERVICE PROVIDER (CODE READY NOT YET USED)
- GEOLOCATION
- USER APP INITIAL
- CURRENT PARTY CHAT CONNECTION STATUS, VOIP STATUS
- CURRENT USER
- APPLICATIONS RUNNING
- DEVICE ID
- PIGEON IDENTITY
- TIME
- IS DEVICE CONNECTED TO THE PHONE
- IS USER HORIZON VERIFIED
- ALL APPLICATION ID, INSTALL TIME, ERRORS, PACKAGE HASH, PACKAGE MANIFEST, PACKAGE PACKAGE SIGNATURES

The device sends this data to thee endpoint htttps://graph.facebook.com/logging_client_events the post packet contains a X-FB debug header alongside a specially crafted user-agent containing information such as:
- FB_APP_NAME = "FBAN";
- FB_APP_VERSION = "FBAV";
- FB_APP_VERSION_MAP = "FBVM";
- FB_BRAND = "FBBD";
- FB_BUILD_VERSION = "FBBV";
- FB_CARRIER = "FBCR";
- FB_CPU_ABI = "FBCA";
- FB_DEVICE = "FBDV";
- FB_DEVICE_WIDE_STATE = "FBDW";
- FB_LOCALE = "FBLC";
- FB_MANUFACTURER = "FBMF";
- FB_PACKAGE_NAME = "FBPN";
- FB_SYSTEM_VERSION = "FBSV";
### GatekeeperService
The GatekeeperService is the service that stores GK sourced server-side via the VRruntimeServer, GK's are systemwide variables that decide whether a device can have access to certain features. The Service uses the com.oculus.permission.WRITE.GKS permission to write GK's to a device.
### VrShell
VrShell is arguably the most important application on the entire device, it manages Cursor Movement, Notifications, System 2D panels, Main nav host, System dialogue, Quick Experiments, Keyboard Rendering, etc. However, found in the application is a code library known as Panelapp, this contains all the panels the user will not see, the panels found within the library are related to Dogfooding, Debug or GauntletTests. The first Panel Dogfood contains information regarding OTA Updates, Developer Settings (ADB & MTP), Current Build, Current system application builds and any assignments a device has been given. A normal user is able to access this Panel by passing a specifically crafted intent. The next panel is Debug, this is an In-House non-user-accessible panel, it checks for certain GK's before running, however, the panel contains the following The adjusting of GK's, System preferences, Shell preferences, Debug preferences, App status, Test actions i.e Local account mode, Controller repair, Disabling of Telemetry, System dialogue debug, and xrsp. VrShell also has enterprise-specific Settings and dialogue.
### VrDriver
VrDriver manages certain system variables i.e 120hz support or hand tracking frequency. The application seems to mostly communicate with VR applications/games regarding additional features or permissions.
### System UX
Runs UX related code, i.e spinners, buttons, checkbox's etc.

[SystemUx Intents as of v29](SystemUX_Intents)
### OSUpdater
Retrieves Latest OS update from Oculus servers and installs the update, Also monitors system vital signs such as battery and wifi. The application logs many details of the update.
### ChargeControl
Application is meant to only be accessible for employes however, with a specialy crafted intent you are able to access the application (com.oculus.os.chargecontrol.action.start or ). The application allows for the limitation of the devices battery capacity. 
### Assistant
The oculus Assistant is a virtual assistant for the quest. The application retrieves a set of preferences from a server, similar to GK'S.

