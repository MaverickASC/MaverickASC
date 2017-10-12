# MaverickASC
# BETA Release: Working version, tested on some devices.
# Still working on getting the device automatically added to Smartthings.
# v 0.1: Got the battery status and device checkin working along with identifying the right device signature.
# v 0.2: Got the structure fixed and more consistent error and debug logging

If you have issues where the Xiaomi Water Leak Sensor is getting recognized at all, the here is what I had to do for it to work:

1. Go to http://ide.smartthings.com and add the Xiaomi Aqara Water Sensor custom Device Handler located in this repository. (a. go to IDE, b. select your location & /or hub, c. go to Device Handlers, d. Click "Create a new device handler" on the right e. Click the TAB "From Code" f. Paste the code in the .groovy file).

2. Look at this thread: https://community.smartthings.com/t/xiaomi-zigbee-outlet-steps-to-pair-any-xiaomi-zigbee-device/67582 for instructions on how to pair Xiaomi devices in general. Keep this information in mind as you are looking for "catchall: " (without quotes) to show up in IDE (http://ide.smartthings.com).

Or look for this entry:

	debug non-TV event zbjoin: {"dni":"**XXXX**","d":"YYYYYYYYYYYYYYYYYYY","capabilities":"80","endpoints":[{"simple":".....................manufacturer":"LUMI","model":"lumi.sensor_wleak.aq1"}],"parent":"FFFF","joinType":255}

You need the value of “XXXX”, so note it down (for lumi.sensor_wleak sensor).

3. Put the hub in pairing mode. These devices do not show up so easily when you put the hub in pairing mode, to say the least, and even if you are trying to locate them in Live Logging (a. go to IDE, b. select your location & hub, c. go to Live Logging page).Alternatively its recommended to use List Events on the HUB (a. go to IDE, b. select your hub, c. go to List Events page) for easily looking for this information. 

NOTE: Not all catchall: can help you identify the device. Some catchall: is related to device metadata and battery information for existing devices. You are looking for catchall: with the device signature like so 

	"01 0104 0402 01 03 0000 0003 0001 01 0019"

in it. So be careful with false positives!

4. Follow the reset & pair process:

		a. Hold the sensor down for some time till the light flashes and then turns off (takes around 1 minute or so). Key point to note that once you let go you should see a single flash (my unit was not showing this behavior, so i improvised).
		b. To complete reset, you need to hold it down again and then wait for the light flash to turn off. Reset completes at this step.
		c. Put it in pairing mode, quick press till it flashes, repeat if does not work (in my case it did not work).
		
5. IMPROVISE:

		a. Remove the battery cover using a penny.
		b. Hold the battery down with your finger and repeat the step 3.
		c. You should see the "catchall: " show up. Close the lid.
		
6. Add the device from IDE using steps mentioned in Step 1. Change the device type to “Xiaomi Aqara Water Sensor” from the list.
7. IMPORTANT: Go back to Smarthings app and “Add a thing” (even if you see the device in the list) and then pair. Pairing should now complete.
8. You now need to establish the link between the sensor and the device by dunking the sensor in a bowl of water filled shallow, just enough to produce the water leak effect!

Using the custom device handler you should be able to get the battery status and also device checkin every 1 hour.
