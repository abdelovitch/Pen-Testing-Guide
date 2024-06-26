# iOS

{% embed url="https://martabyte.github.io/ios/hacking/2022/03/13/ios-hacking-en.html" %}

```bash
# All about Jailbreak & iOS versions
https://www.theiphonewiki.com/wiki/Jailbreak

# OWASP MSTG
https://github.com/OWASP/owasp-mstg

# Jailbreak list
https://docs.google.com/spreadsheets/d/11DABHIIqwYQKj1L83AK9ywk_hYMjEkcaxpIg6phbTf0/edit#gid=1014970938

# Checklist
https://mobexler.com/checklist.htm#ios

# Jailbreak for iPhone 5s though iPhone X, iOS 12.3 and up
# https://checkra.in/
checkra1n 

# 3UTools
http://www.3u.com/

# Cydia
# https://ryleylangus.com/repo
# Liberty Bypass Antiroot

# SSL Bypass
# https://github.com/evilpenguin/SSLBypass


# Check Info Stored:
3U TOOLS - SSH Tunnel

# Analyzing binary:
# Get .ipa
# unzip example.ipa
# Locate binary file (named as the app usually)

# Check encryption
otool –l BINARY | grep –A 4 LC_ENCRYPTION_INFO
# If returned "cryptid 1" ipa is encrypted, good for them

# Check dynamic dependencies
otool –L BINARY

# Using plutil to modify properties
# https://scriptingosx.com/2016/11/editing-property-lists/

# SSL Bypass
# https://github.com/evilpenguin/SSLBypass

find /data/app -type f -exec grep --color -Hsiran "FINDTHIS" {} \;
find /data/app -type f -exec grep --color -Hsiran "\"value\":\"" {} \;

.pslist= "value":"base64"}

find APPPATH -iname "*localstorage-wal" -> Check manually

# Extract IPA from installed app
# https://github.com/AloneMonkey/frida-ios-dump
# Manual way (without launching the app)
ls -lahR /var/containers/Bundle/Application/ | grep -B 2 -i 'appname' # To find app ID
scp -r root@127.0.0.1:/var/containers/Bundle/Application/{ID} LOCAL_PATH
mkdir Payload
cp -r appname.app/ Payload/
zip -r app.ipa Payload/

# Objective-C and Swift class dumper
# https://github.com/DerekSelander/dsdump

# Interesting locations
/private/var/mobile/Containers/Data/Application/{HASH}/{BundleID-3uTools-getBundelID}
/private/var/containers/Bundle/Application/{HASH}/{Nombre que hay dentro del IPA/Payloads}
/var/containers/Bundle/Application/{HASH}
/var/mobile/Containers/Data/Application/{HASH}
/var/mobile/Containers/Shared/AppGroup/{HASH}
```

![](<../.gitbook/assets/image (34).png>)
