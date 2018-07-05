SETUP:
======

ionic platform add android ios


CREATE NEW APP:
ionic start MobileApp

RUN ON BROWSER:
ionic serve


RUN APP ON IOS SIM:
ionic build ios
ionic emulate ios

*RUN APP ON IOS DEVICE !!:*
ionic run ios --device


Build www files into xcodeproj:
cordova prepare ios



INSTALL IOS SIM:
npm install -g ios-sim



cordova plugin add https://github.com/Wizcorp/phonegap-facebook-plugin.git --variable APP_ID="xxx" --variable APP_NAME="xxx"


cordova plugin remove phonegap-facebook-plugin


https://github.com/ccoenraets/OpenFB


STATUS BAR:
cordova plugin add cordova-plugin-statusbar

#IONICS Reference#

## ionic commands ##
https://github.com/driftyco/ionic-cli#update-ionic-lib




RELEASE:
===================
ionic build ios

sudo ionic build ios

ionic build android

sudo ionic build android


TESTING:
===================
ionic run ios --device


with live reload and console:
ionic run ios --device -l -c




TESTING SIM:
===================

ionic emulate ios


Emulate with live reload:
ionic emulate ios -l 


Emulate on iPhone4:
ionic emulate ios --target="iPhone-4s"


OTHERS:
===================
To generate icon, splash screen:
ionic resources


To find out available emulations I run this:
ios-sim showdevicetypes


ionic platform rm ios

ionic platform add ios