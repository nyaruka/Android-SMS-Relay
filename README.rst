Android SMS Relay
=================

This is a simple SMS relayer.  It essentially turns your Android phone into an SMS modem that will relay messages to an HTTP server of your choice and vice versa.

We use this quite a bit in our work, so we thought we'd open it up to the world.  Note that this particular codebase is still pretty Alpha and we've been cleaning it up for the outside world.  It very well might break, but we appreciate any and all testing and bug reports.

Things that make it different than other solutions:

* we are backed by a database for persistence, we think that makes it less likely a message will be dropped in the case of power outages, reboots, or other issues
* we have a prettier message UI than the other guys
* we will toggle Wifi on or off in the case of network errors.. this can be useful in places where WiFi is not reliable as the phone will then back down to GSM when it is acting up (and automatically switch back to WiFi when it starts working again)
* easy integration with our RapidSMS httprouter module. (http://github.com/nyaruka/rapidsms-httprouter)

This is still pretty early stuff, so any feedback or bug reports much appreciated.

INSTALL
=======

You can build this yourself if you'd like, you'll need version 3.* of actionbar-sherlock though.  Until we hit the market, I'd recommend using the pre-build APK at: 
    https://github.com/downloads/nyaruka/android-sms-relay/android-sms-relay.apk

.. image:: https://chart.googleapis.com/chart?cht=qr&chs=300x300&chl=https://github.com/downloads/nyaruka/android-sms-relay/android-sms-relay.apk

TODO
=====

* Allow user to configure a regex for which messages to handle (ie, only those starting with a particular keyword)
* Allow configuration of the handset via a file attachment, could make client configuration easier
* Even more reliability / paranoia updates to make sure a message never gets lost
* Remove messages from the SMS inbox

LICENSE
==========

Android SMS Relay is licensed under the GPL v3.  You are free to modify and distribute this software, and modify it as you see fit.  You can even charge for it, but you must make the source code freely available forr anybody to download.  Note that you cannot use any part of this software without falling under the license, please refer to LICENSE.txt for details.

CHANGELOG
==========

0.0.5
-----
* Replaced Sherlockactionbar with Android Actionbarcompatibility
* Change password through the preferences
* Use password as preference incoming keyword
* Set preferred network through preferences
* Change preferred network using sms e.g "password data|wifi"
* The preferred network will take effect based on the next update interval
* Clear messages using sms e.g "password clear"
* The process to tickle airplane mode and when to do so
* Always tickle the default APN to make sure that after airplane the Mobile data is perfectly working
* Removed the airplane hack in the preference
* Replaced the airplane mode hack with the ability to send sms to reset e.g "password reset"

0.0.4
-----
* add an empty view when first entering the app, slightly prettier
* allow separately toggling whether any outgoing messages from the server will be processed
* fix a bug where refresh intervals > 30 mins wheren't taking effect

0.0.3
------
* switch to use ActionBar Sherlock so we can have a consistent 4.0+ look to the app.  Doesn't look uber pretty on 2.3 devices, but it is ok and much better than Nyaruka banner
* new silly icon, better than Nyaruka icon
* tweak the WiFi/GSM backdown so that it'll work when the phone is tethering to a local IP.  We used to check against Google.com, now we strictly start toggling based on IOExceptions to our endpoints.  So it'll work in an isolated environment still. (todo, make this configurable?)
* kick the sync service when we get SENT notifications, causing the server to be up to date more quickly

0.0.2
-------
* try to ping google.com before accessing server, if it fails, flip our WiFi state (from off to on or vice versa) then try again, restoring the state at the end
* trim our database to most recent 100 messages which have been handled
* fix a nasty bug with deliveries
* add RapidSMS endpoint configuration
* other little fixes

0.0.1
--------
* Initial release
