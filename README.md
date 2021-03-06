# vesync-wsproxy
A little proxy for the websocket connection used by etekcity wifi outlets

### Setup

The setup process is a little annoying. You'll need your local DNS server to return 
the IP address of the server hosting this proxy for the hostname "server2.vesync.com".
You'll then need to make sure your server is still able to resolve server2.vesync.com correctly.  

Once that's done and your proxy is running, you may need to power cycle the outlet to encourage it 
to find your server.

### General Goals
- enable the outlet to remain "smart" if the server goes offline (the outlet already remembers configured timers, but it would lose the ability to be turned on/off or configured.)  
- watch and validate the network traffic between the outlet and some strange server (block unrecognized traffic over the websocket by default. /upgrade is technically recognized, but still blocked.)  
- enable integration of the outlet with other environments. The service port can be targeted with IFTTT's Maker channel to take actions, and that concept can be extended further.

### Non-goals
- replace the mobile app. Yes, it's a quirky app, but I don't really see myself committing to rewrite the whole thing.  
- develop custom firmwares. This proxy allows to spoof an /upgrade packet which will trigger an OTA firmware update. But without some other way to reset the firmware, this is likely to result in a brick. No go for now.  
( However this is really just an ESP8266 shaped like a plug. There are whole communities of people that write firmware for this stuff out there.)

### Miscellaneous Random Notes

- 5 seconds push => solid blue light = airkiss/esptouch/whatever mode  
  -> in this mode, the device sniffs UDP packets sent to (its own, or some agreed upon) BSSID, and derive a data stream from UDP packet lengths, presumably  
  -> that means your wifi password goes in plain text over the air, for anybody listening to grab.  
  ( I wish I knew how to sniff that, to see the shape of that data stream exactly. )

- ~30 seconds push => blinking blue light = "APN" mode. The device broadcasts a BSSID named "ESP\_xxxxxx" where xxxxxx are the last digits of its MAC address. The mobile app can be made to target that BSSID (by matching the ESP\_ prefix?)


