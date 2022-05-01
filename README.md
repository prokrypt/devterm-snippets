Brightness up<br>
```echo $((`cat /sys/class/backlight/backlight@0/brightness`+1)) > /sys/class/backlight/backlight@0/brightness```

Brigntness down, with ugly hack to prevent 0 brightness<br>
```echo $(((`cat /sys/class/backlight/backlight@0/brightness`-1)*9/10+1)) > /sys/class/backlight/backlight@0/brightness```

Possibly cleaner version of brightness up with no external commands<br>
`bl="/sys/class/backlight/backlight@0/brightness"; read br < $bl; echo $((br+1)) > $bl`

Possibly cleaner version of brightness down with no external commands<br>
`bl="/sys/class/backlight/backlight@0/brightness"; read br < $bl; echo $(((br-1)*9/10+1)) > $bl`

Change suspend mode to s2idle<br>
`tee /sys/power/state <<< s2idle`

Turn off all cores except core "0"<br>
`tee /sys/devices/system/cpu/cpu[12345]/online <<< 0`

Turn on all cores<br>
`tee /sys/devices/system/cpu/cpu?/online <<< 1`

Switch governor of both cluters to conservative<br>
`tee /sys/devices/system/cpu/cpufreq/policy?/scaling_governor <<< conservative`

Get available frequencies and governors<br>
`grep . /sys/devices/system/cpu/cpufreq/policy?/*avail*`
