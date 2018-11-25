# YamahaExtendedControl Protocol

Yamaha HTTP simplified API for Control Systems
V1.1 - June 20, 2017

## Overview

Yamaha provide a comprehensive API for control and interrogation of MusicCast devices.
This document covers the most useful features, with examples, for integration in to CI
Environments.

## Prerequisites/Recommendations

For the HTTP API to function correctly in an integrated system, the MusicCast devices must
be on a fixed or bound IP Address. To avoid network loops through the wireless “extend”
functionality of MusicCast products you should set the device to wired or wireless only -
through the web GUI on the MusicCast device:

## HTTP API Overview

All HTTP transactions take place through a connection to the MusicCast device on port 80
(the default used by a web browser), and take the following form:
HTTP:// [ipaddress] /YamahaExtendedControl/v1/...
Example:
http://[ipaddress]/YamahaExtendedControl/v1/system/getFeatures
(recalls the available features on the MusicCast device)


## HTTP API - Get information

Note that when a zone is specified below, the available zones per device can be recalled
using the getLocationInfo command. In all examples main has been used.
Get Device info http://[ipaddress]/YamahaExtendedControl/v1/system/getDeviceInfo
Get Available Device Features http://[ipaddress]/YamahaExtendedControl/v1/system/getFeatures
Get Network Status http://[ipaddress]/YamahaExtendedControl/v1/system/getNetworkStatus
Get Function Status (e.g.: Auto Power Standby) http://[ipaddress]/YamahaExtendedControl/v1/system/getFuncStatus
Get Location info and zone list (device) http://[ipaddress]/YamahaExtendedControl/v1/system/getLocationInfo
Get zone info (device|zone) http://[ipaddress]/YamahaExtendedControl/v1/main/getStatus
Get Sound Program List (device|zone) http://[ipaddress]/YamahaExtendedControl/v1/main/getSoundProgramList

## HTTP API - Power Functions

Enable/Disable Auto Power http://[ipaddress]/YamahaExtendedControl/v1/system/setAutoPowerStandby?enable=true
Standby http://[ipaddress]/YamahaExtendedControl/v1/system/setAutoPowerStandby?enable=false
Power on http://[ipaddress]/YamahaExtendedControl/v1/main/setPower?power=on
Standby http://[ipaddress]/YamahaExtendedControl/v1/main/setPower?power=standby
Power Toggle http://[ipaddress]/YamahaExtendedControl/v1/main/setPower?power=toggle

## HTTP API - Sleep Timer

Set in minutes. Use zone name from getLocationInfo
Set Sleep timer for 60 minutes http://[ipaddress]/YamahaExtendedControl/v1/main/setSleep?sleep=60
Cancel Sleep timer http://[ipaddress]/YamahaExtendedControl/v1/main/setSleep?sleep=0

## HTTP API - Input and Volume

Input: Net Radio http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=net_radio
Input: Napster http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=napster
Input: Spotify http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=spotify
Input: Juke http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=juke
Input: Qobuz http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=qobuz
Input: Tidal http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=tidal
Input: Deezer http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=deezer
Input: Server http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=server
Input: Bluetooth http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=bluetooth
Input: Airplay http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=airplay
Input: MusicCast link http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=mc_link
The functions in the table above use autoplay to start the last item playing if the source is
not already playing. Alternatively the autoplay_disabled function can be used:
http://[ipaddress]/YamahaExtendedControl/v1/main/setInput?input=airplay&mode=autoplay_disabled
Prepare Input Change (not necessary for direct input changes)
Let a Device do necessary process before changing input in a specific zone. This is valid
onlywhen “prepare_input_change” exists in “func_list” found in /system/getFuncStatus. 
http://[ipaddress]/YamahaExtendedControl/v1/main/prepareInputChange?input=usb
Set Sound Program (where applicable) http://[ipaddress]/YamahaExtendedControl/v1/main//setSoundProgram?program=vienna

### Volume Commands

For the Direct Volume function, the maximum volume setting available can be obtained from
/system/getFeatures. For the stepped volume function thestep ranges are shown in the
volume section of /system/getFeatures. 

Direct Volume http://[ipaddress]/YamahaExtendedControl/v1/main/setVolume?volume=60
Incremental http://[ipaddress]/YamahaExtendedControl/v1/main/setVolume?volume=up
http://[ipaddress]/YamahaExtendedControl/v1/main/setVolume?volume=down
In Steps http://[ipaddress]/YamahaExtendedControl/v1/main/setVolume?volume=up&step=5
http://[ipaddress]/YamahaExtendedControl/v1/main/setVolume?volume=down&step=1

### Mute Commands

Set Mute On http://[ipaddress]/YamahaExtendedControl/v1/main/setMute?enable=true
Set Mute Off http://[ipaddress]/YamahaExtendedControl/v1/main/setMute?enable=false

## HTTP API - AM/FM/DAB Tuner Commands

Tuner Presets
Where band can be am, fm or dab
Recall Preset http://[ipaddress]/YamahaExtendedControl/v1/tuner/recallPreset?zone=main&band=fm&num=13
Next Preset http://[ipaddress]/YamahaExtendedControl/v1/tuner/switchPreset?dir=next
Previous Preset http://[ipaddress]/YamahaExtendedControl/v1/tuner/switchPreset?dir=previous
Store Preset http://[ipaddress]/YamahaExtendedControl/v1/tuner/storePreset?num=10
Get Preset info http://[ipaddress]/YamahaExtendedControl/v1/tuner/getPresetInfo?band=fm
Tuner - Get Playing info http://[ipaddress]/YamahaExtendedControl/v1/tuner/getPlayInfo
Tuner - Set Frequency
Where num represents frequency in KHz
http://[ipaddress]/YamahaExtendedControl/v1/tuner/setFreq?band=fm&tuning=direct&num=87500

## Tuner - Change DAB Service

Next Service http://[ipaddress]/YamahaExtendedControl/v1/tuner/setDabService?dir=next
Previous Service http://[ipaddress]/YamahaExtendedControl/v1/tuner/setDabService?dir=previous
http://[ipaddress]/YamahaExtendedControl/v1/tuner/setFreq?band=fm&tuning=direct&num=87500

## HTTP API - Network/USB Presets and info

Recalls presets for any network or USB-based service. Playing info includes all metadata and
image link
Get Preset info http://[ipaddress]/YamahaExtendedControl/v1/netusb/getPresetInfo
Get Current Playing info http://[ipaddress]/YamahaExtendedControl/v1/netusb/getPlayInfo
Get Account Status (streaming services) http://[ipaddress]/YamahaExtendedControl/v1/netusb/getAccountStatus

## HTTP API - System Presets

Recalls presets for the MusicCast system. Use zone name from getLocationInfo .
Recall Preset http://[ipaddress]/YamahaExtendedControl/v1/netusb/recallPreset?zone=main&num=2
Store Preset http://[ipaddress]/YamahaExtendedControl/v1/netusb/storePreset?num=10

## HTTP API - Transport Control

Sets Playback or transport mode.
Stop http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=stop
Play http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=play
Previous http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=previous
Next http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=next
Fast Rewind - Start http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=fast_reverse_start
Fast Rewind - Stop http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=fast_reverse_end
Fast Forward - Start http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=fast_forward_start
Fast Forward - Stop http://[ipaddress]/YamahaExtendedControl/v1/netusb/setPlayback?playback=fast_forward_end
Repeat (Toggle) http://[ipaddress]/YamahaExtendedControl/v1/netusb/toggleRepeat
Shuffle (Toggle) http://[ipaddress]/YamahaExtendedControl/v1/netusb/toggleShuffle

## HTTP API - List info

Retrieve metadata and list entries. input is Input ID from /system/getFeatures | index is list
offset from beginning | size is maximum list size 1-8)
http://[ipaddress]/YamahaExtendedControl/v1/netusb/getListInfo?input=usb&index=32&size=8&lang=en
