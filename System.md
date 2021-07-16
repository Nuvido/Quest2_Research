# Quest Research
## Background Information
The Oculus Quest 2 is a HMD running the Snapdragon XR2. The device runs on a highly modified version of Android 10, running the 2020 September security patch.
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

## A note about the Quest 2
The Quest 2 Formally is running the XR2 However, code libaries suggest it is infact running the sm8250 (Qualcomm 865 5G), This could reason that the Quest 2 was originally developed for the sm8250 and then switched to the XR2.

## Analysing The Firmware 
 
### Recovery Image
Similarly to other android devices, android OTA updates come in two forms incremental or full. Full updates are easier to analyze as they don't rely on previously existing updates. To start off with, let's begin with the recovery image. The recovery image contains information, code, and images related to the device if it was in a "Bare-bones" state. Using Carliv image kitchen, we can unpack the image to see its contents. With this recovery image there are only (IDK) files populated, the first of which is ODM, which contains information of the location of other files, the next populated file is RES, this file contains the images you would see when you put your device in recovery, below are the images found within the file. The next populated file is system. System contains bin commands alongside OTA-Certs.

### System Image
The system image is very similar to the recovery image in its structure, however, it contains a lot more information and files. Some of the more important information can be found below.
- [Default Props](prop.default)


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

The device sends this data to thee endpoint https://graph.facebook.com/logging_client_events the post packet contains a X-FB debug header alongside a specially crafted user-agent containing information such as:
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
##### A closer analysis of a Logging Event 
An example of an average post request can be found [here](exmp), a closer analysis reveals some intresting information.
- Oculus have unlocked devices
- Oculus have devices with custom bootloaders
- Oculus use a sandbox system similar to instangram 
- Oculus have multiple log types
- Multiple device types (User, dev and internal)
- The user is called twsvcscm
### GatekeeperService
The GatekeeperService is the service that stores GK sourced server-side via the VRruntimeServer, GK's are systemwide variables that decide whether a device can have access to certain features. The Service uses the com.oculus.permission.WRITE.GKS permission to write GK's to a device.
#### Why GK's are Important
GK's can been seen in all Oculus software, this includes The desktop app, the mobile app and headset. GK's often reveal information regarding new features that are only enabled on internal devices, the GK's can also enable updates and Killswitch's.
#### An example of a GK Request and Response
The application on launch will send GET request to the [url](https://graph.facebook.com/v11.0/1517832211847102/mobile_sdk_gk?fields=gatekeepers&format=json&sdk_version=11.0.0&sdk=android&platform=android) with fields stating the SDK version and platform, the server will then respond with the following [headers](header) and the following [response](respo) 

### VrShell
VrShell is arguably the most important application on the entire device, it manages Cursor Movement, Notifications, System 2D panels, Main nav host, System dialogue, Quick Experiments, Keyboard Rendering, etc. However, found in the application is a code library known as Panelapp, this contains all the panels the user will not see, the panels found within the library are related to Dogfooding, Debug or GauntletTests. The first Panel Dogfood contains information regarding OTA Updates, Developer Settings (ADB & MTP), Current Build, Current system application builds and any assignments a device has been given. A normal user is able to access this Panel by passing a specifically crafted intent. The next panel is Debug, this is an In-House non-user-accessible panel, it checks for certain GK's before running, however, the panel contains the following The adjusting of GK's, System preferences, Shell preferences, Debug preferences, App status, Test actions i.e Local account mode, Controller repair, Disabling of Telemetry, System dialogue debug, and xrsp. VrShell also has enterprise-specific Settings and dialogue.
### VrDriver
VrDriver manages certain system variables i.e 120hz support or hand tracking frequency. The application seems to mostly communicate with VR applications/games regarding additional features or permissions.
### System UX
Runs UX related code, i.e spinners, buttons, checkbox's etc.

[Systemux Intents as of v29](SystemUX_Intents)
### OSUpdater
Retrieves Latest OS update from Oculus servers and installs the update, Also monitors system vital signs such as battery and wifi. The application logs many details of the update.
### ChargeControl
Application is meant to only be accessible for employes however, with a specialy crafted intent you are able to access the application (com.oculus.os.chargecontrol.action.start or ). The application allows for the limitation of the devices battery capacity. 
### Assistant
The oculus Assistant is a virtual assistant for the quest. The application retrieves a set of preferences from a server, similar to GK'S.
### YADI
Yadi is a service/application installed on every quest device, it fullfils the need for internal package installation and updating. It allows for facebook to deploy applications on internal devices. An intresting note is that the application refers to itself as YadiOs
### Device Auth Server
This application pings the url graph.facebook-hardware.com and requests for a token (sha256WithRSAEncryption) internal versions of the device allow for a different sandbox to be used as with the structure "graph." + sandbox + ".facebook-hardware.com". Debug devices ping ovr.deviceauth.sandbox.facebook-hardware.com
### Oculus Bug Reporter
As the name implies this is the service responsible for user bug reports. When a bug report is intiated it checks the following.
- is productivity_mode_enabled
- Using Infinite Office Platform
- User description
- All system application versions
It will then send a post packet to the url https://graph.oculus.com/report_bug This packet contains the above information and more.
### QALAB
Not much is known about this application as it is not user accessible. The only user facing part of this application is a reset service which resets the device after a counter counts down from 5 Minutes The service is com.oculus.qalab\
### Stats Collector
As the name implies, it collects stats from the device. Stats such as the following are collected.
- oculus_mobile_disk_io_by_uid
- culus_mobile_lmk_kill_events
- oculus_mobile_low_storage_events
- oculus_mobile_thermal_throttling_events
- oculus_mobile_wall_clock_events
- oculus_mobile_wifi_enabled_events
- Various BLE information
### Companion Server
Companion server is an admin application that manages the device and does the following.
- Controlls controllers and monitors vital signs
- Manages OS updater Intents
- Manages screen shoots and videos
- Tells other applications what the current HMD is capable of, in a software view
- Sends Data to Oculus mobile application
- Manages BT connection with TWILIGHT (Mobile oculus app)
- Manages Anti Piracy Kill Switch
- Phone Notifications & Analytics on those notifications
### UserServer Version 1 & 2
Manages device users and settings such as application sharing, or syncing or user information. 
### Mixed Reality
The application only checks whether a specific GK is enabled, has to do with AR
### Enterprise Server
The Enterprise Server is an application installed on all quests, if a buisness where to purchase the Enterprise server, oculus would change a GK within the device Enterprise server. The server communicates mostly towards the web facing portal for the management and deployment of the quest. Allows for the adjusting of these settings.
- Whiteboard Guardian
- Swapping of controller buttons
- Update Scheldules
- Remote wipe
### Vr Alert Services
Alerts the user if any emergency events are occuring on the device. for example, if a device overheats this service is called. The following alerts are managed by the service.
- Fan malfunction
- Thermal Alerts
### Explore App
When a user firsts boots their vr headset this is the first panel a user will see. Application has mentions of Pass Through filters. The intent to launch the application is apk://com.oculus.explore
