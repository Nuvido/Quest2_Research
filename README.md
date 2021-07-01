# Quest2_Research
## Background Information
The oculus quest 2 is a HMD running the Snapdragon XR2. The device runs on a highly modified version of Android 10, running the 2020 September security patch.
##Glossary
Throughout this research, you may come across a few quest specific abbreviations or terms.
- OCMS (Oculus Media Services)
- NUX (New User Experience)
- GK (Gatekeeper)
- Telemetry (Tracking)
- Horizon (Social Services)
## App Signatures

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

