# Linux WiFi drop issue due to battery saving

## Problem
Even though I see my network connection as active, I noticed that sometimes my WiFi connection will just stop working and pause whatever I'm in the middle of. If I am watching a YT video, it'll stop loading. If I'm in a Zoom call, the video will just pause mid-way (MAJOR PROBLEM).

I had to reset my network connection (turning off and back on) each time to resolve the issue.

## Root Cause
The issue was caused by Intel's power-saving features disabling the Wi-Fi interface to conserve battery. Since my ThinkPad T480 has degraded internal and external batteries, it likely triggered this behavior more aggressively than normal.

### Example Log
```
boosung@terra:~$ sudo dmesg | grep iwlwifi
[   18.268684] iwlwifi 0000:03:00.0: firmware: direct-loading firmware [firmware file]
[   18.269218] iwlwifi 0000:03:00.0: loaded firmware version [firmware internal build ID] [firmware file] op_mode iwlmvm
[   18.498522] iwlwifi 0000:03:00.0: Detected [chip model info]
[   18.571113] iwlwifi 0000:03:00.0: base HW address: [MAC address], OTP minor version: [version id]
[ 2918.786066] (NULL device *): firmware: direct-loading firmware [firmware file]
[ 8109.640493] (NULL device *): firmware: direct-loading firmware [firmware file]
...
```

The repeating `(NULL device *)` lines suggest the firmware was being reloaded, likely due to device reset or power management kicking in.

## Solution
1. `sudo nano /etc/modprobe.d/iwlwifi.conf`
2. Add `options iwlwifi power_save=0`.
3. Reboot OR `sudo modprobe -r iwlwifi && sudo modprobe iwlwifi`.

## Result
After the fix, the `(NULL device *)` messages disappeared, and I haven’t experienced any random network drops since. Likely resolved.

```
boosung@terra:~$ sudo dmesg | grep iwlwifi
[   12.006875] iwlwifi 0000:03:00.0: firmware: direct-loading firmware [firmware file]
[   12.010275] iwlwifi 0000:03:00.0: loaded firmware version [firmware internal build ID] [firmware file] op_mode iwlmvm
[   12.350251] iwlwifi 0000:03:00.0: Detected [chip model info]
[   12.424746] iwlwifi 0000:03:00.0: base HW address: [MAC address], OTP minor version: [version id]
```