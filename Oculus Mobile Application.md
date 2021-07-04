# Oculus Mobile Application (Twilight)
The Oculus mobile application is the application a user would install on there phone for the setting up,customization or casting of a device. Currently There are three known build types of the app.

- twilight-dev https://m.intern.facebook.com/intern/mobile_builds/
- twilight-inhouse https://m.intern.facebook.com/intern/mobile_builds/
- twilight-prod https://play.google.com/store/apps/details?id=com.oculus.twilight

OTA updates for application and Quest are sourced using the following structure

\String str3 = "update" + "%7B" + "download_uri" + "%2C" + "download_uri_delta_base" + "%2C" + "version_code_delta_base" + "%2C" + "download_uri_delta" + "%2C" + "fallback_to_full_update" + "%2C" + "file_size_delta" + "%2C" + "version_code" + "%2C" + "published_date" + "%2C" + "file_size" + "%2C" + "ota_bundle_type" + "%2C" + "resources_checksum" + "%2C" + "resources_sha256_checksum" + "%2C" + "allowed_networks" + "%2C" + "release_id" + "%7D";

When a user intial Logins to the application a Facebook access token is retreived from this url https://graph.oculus.com/facebook_access_token_generate

