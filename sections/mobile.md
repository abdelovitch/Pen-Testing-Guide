# Mobile

## General

```text
# Frida
# https://github.com/frida/frida/releases
adb push C:\Users\username\Downloads\frida-server-12.8.11-android-arm /data/local/tmp/.

Objection
https://github.com/sensepost/objection

MobSF
docker pull opensecurity/mobile-security-framework-mobsf
docker run -it -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest

Burp
Add proxy in Mobile WIFI settings connected to Windows Host Wifi pointing to 192.168.X.1:8080
Vbox Settings Machine -> Network -> Port Forwarding -> 8080
Burp Proxy -> Options -> Listen all interfaces

Tools
https://github.com/tanprathan/MobileApp-Pentest-Cheatsheet
https://github.com/m0bilesecurity/RMS-Runtime-Mobile-Security
```

## Android

```text
# Adb
# https://developer.android.com/studio/command-line/adb?hl=es-419
adb connect IP:PORT/ID
adb devices
adb shell
adb push
adb install

# Analyze URLs in apk:
# https://github.com/shivsahni/APKEnum
python APKEnum.py -p ~/Downloads/app-debug.apk

# AndroPyTool:
# https://github.com/alexMyG/AndroPyTool
docker pull alexmyg/andropytool
docker run --volume=:/apks alexmyg/andropytool -s /apks/ -all

# Android Backup files (*.ab files)
( printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" ; tail -c +25 backup.ab ) |  tar xfvz -

# https://github.com/viperbluff/Firebase-Extractor
# https://github.com/Turr0n/firebase
python3 firebase.py -p 4 --dnsdumpster -l file

# Frida
# Load Frida Server in device && run objeciton
adb root
adb push /root/Downloads/frida-server-12.7.24-android-arm /data/local/tmp/.
adb root
adb shell "chmod 755 /data/local/tmp/frida-server && /data/local/tmp/frida-server &"
frida -U -f com.vendor.app.version -l PATH\fridaGlomoPR.js --no-pause

objection --gadget com.vendor.app.xx explore

# Run JS script in Frida
frida -U -l script.js com.vendor.app.version --no-pause

# Jadx - decompiler
jadx-gui

# androwarn.py
# pip3 install androwarn
androwarn /root/android.apk -v 3 -r html

# androbugs.py
python androbugs.py -f /root/android.apk

# Userful apps:
# Xposed Framework
# RootCloak
# SSLUnpinning

# Check Info Stored
find /data/app -type f -exec grep --color -Hsiran "FINDTHIS" {} \;

/data/data/com.app/database/keyvalue.db
/data/data/com.app/database/sqlite
/data/app/
/data/user/0/
/storage/emulated/0/Android/data/
/storage/emulated/0/Android/obb/

# Check logs during app usage
https://github.com/JakeWharton/pidcat

# Download apks
https://apkpure.com

Recon:
- AndroidManifest.xml (basically a blueprint for the application)
Find exported components, api keys, custom deep link schemas, schema endpoints etc.
- resources.arsc/strings.xml
Developers are encouraged to store strings in this file instead of hard coding in application.
- res/xml/file_paths.xml
Shows file save paths.
- Search source code recursively
Especially BuildConfig files.

API Keys:
- String references in Android Classes
getString(R.string.cmVzb3VyY2VzX3lv)
cmVzb3VyY2VzX3lv is the string resource label.
- Find these string references in strings.xml
apikeyhere
- Piece together the domains and required params in source code

Exported components:
- Activities - Entry points for application interactions of components specified in AndroidManifest.xml.
    Has several states managed by callbacks such as onCreate().
   →  Access to protected intents via exported Activities
    One exported activity that accepts a user provided intent can expose protected intents.
   → Access to sensitive data via exported Activity
    Often combined with deep links to steal data via unvalidated parameters. Write session tokens to an
    external file.
   → Access to sensitive files, stealing files, replacing imported files via exported Activities
    external-files-path, external-path
    Public app directories
- Service - Supplies additional functionality in the background.
   → Custom file upload service example that is vulnerable because android:exported="true". When exported by third party
  applications can send data to the service or steal sensitive data from applications depending on the services   function. Check if params and intent data can be set with proof of concept application.
- Broadcast receivers - Receives broadcasts from events of interest. Usually specified broadcasted intents in the broadcast receiver activity.
   → Vulnerable when receiver is exported and accepts user provided broadcasts.
- Content providers - Helps applications manage access to stored data and ways to share data with other Android applications
   → Content providers that connect to sqlite can be exploited via SQL injection by third party apps.

Deep links
- In Android, a deep link is a link that takes you directly to a specific destination within an app.
- Think of deep links as Android urls to specific parts of the application.
- Usually mirrors web application except with a different schema that navigate directory to specific Android activities.
- Verified deep links can only use http and https schemas. Sometimes developers keep custom schemas for testing new
features.
- Type of vulnerabilities are based on how the scheme://, host://, and parameters are validated
   → CSRF - Test when autoVerify=”true” is not present in AndroidManifest.xml It’s easier.
   → Open redirect - Test when custom schemes do not verify endpoint parameters or hosts
   → XSS - Test when endpoint parameters or host not validated, addJavaScriptInterface and
   → setJavascriptEnabled(true); is used.
   → LFI - Test when deep link parameters aren’t validated. appschema://app/goto?file=
```

![](../.gitbook/assets/image%20%283%29.png)

## iOS

```text
# All about Jailbreak & iOS versions
https://www.theiphonewiki.com/wiki/Jailbreak

# Jailbreak for iPhone 5s though iPhone X, iOS 12.3 and up
# https://checkra.in/
checkra1n 

# 3UTools
http://www.3u.com/

# Cydia
# Liberty Bypass Antiroot

# Check Info Stored:
3U TOOLS - SSH Tunnel


find /data/app -type f -exec grep --color -Hsiran "FINDTHIS" {} \;
find /data/app -type f -exec grep --color -Hsiran "\"value\":\"" {} \;

.pslist= "value":"base64"}

find APPPATH -iname "*localstorage-wal" -> Mirar a mano

/private/var/mobile/Containers/Data/Application/{HASH}/{BundleID-3uTools-getBundelID}
/private/var/containers/Bundle/Application/{HASH}/{Nombre que hay dentro del IPA/Payloads}
/var/containers/Bundle/Application/{HASH}
/var/mobile/Containers/Data/Application/{HASH}

# IDB
https://github.com/dmayer/idb
```
