# LinkPlay API Documentation
## Get Information

http://$ReceiverIpAddress/httpapi.asp?command=getStatus


- Description:
Obtain basic information about the device, such as ssid, the version of Equipment, IP wifi and IP Ethernet, etc.

- Supported Formats: JSON
- HTTP Request: GET
- Command: getStatus


Response:

	{
		"Language": "en_us",
		"Ssid": "FA5100_a4dc",
		"Firmware": "WIFIAudio.multil_room.1.2.20140324",
		"Builddate": "release",
		"Release": "20140324",
		"Group": "",
		"Expired": "0",
		"Internet": "0",
		"Uuid": "FF123456nnnnnnnnnnnn",
		"Netstat": "0",
		"Essid": "",
		"Apcli0": "",
		"Eth2": "192.168.120.112",
		"Hardware": "Wi Mu-A03",
		......
	}


Description of Fields:


Fields | Description
-------|------------
Language | Language
SSID | SSID equipment
Firmware | Software version
Build | Note: Actual output is output, debug, save Three cases, indicates the version of the type generally press.
Release | Date of Release
Group | Name of the group
Expired | Outdated software flag: 0: valid; 1: Out of date
MAC | Mac Address
Internet | Internet access: 0; 1: true
Uuid | UDID device, the first 8 bytes of the project ID, followed by the device's unique identifier
Netstat | WIFI connection state. <br>0: not connected <br>1: transient state<br>2: Connected
Essid | WIFI router to connect to, use the command GetStatus returned using hex coded hex to support the transmission of special characters.
Apcli0 | The IP address of WIFI
Eth2 | IP address of the Ethernet
Hardware | Hardware version
Project | Name of the project
VersionUpdate | New version available
NewVer | Available version number
Mcu_ver | The version MCU, if 0 indicates the absence of MCU
DeviceName | Name upnp and airplay of Sonoé iEast
Temp_uuid |  Temp uuid, will change after boot up
Streams | Bit:<br>0 if MFI airplay activated<br>1 airplay activated<br>2 if DLNA enabled<br>3 if Qplay<br>10 if TTPod<br>11 if DoubanFM<br>14 if QingTing<br>15 if ximalaya<br>16 TuneIn<br>17 iHeartRadio<br>18 Tida<br>21 Pandora<br>22 Spotify
Streams_all| The audio streams to be displayed showing the user interface
External| Have a light control
Preset_key | Presets key number
Plm_support | 0 LineIn (Aux)<br>1 BT<br>2 optical
WifiChannel | WiFi Channel WiFi bands
AP_clients | number of AP clients
battery |1 means battery is in charging
Battery_percent | 0 to 100
Securemode | WiFi secured or not
psk | If the WiFi is secured, allows to fill in the password
usb_storagesize | U disk storage size
usb_freesize | Udisk free size
mmc_storagesize | Mmc storage size , otherwise this one, there are no T cards
mmc_freesize | Mmc free size
Part1_storage | User1 part in ROM, storage size
Part1_free | User1 part in ROM, free size
Part2_storage | User2 part in ROM, storage size
Part2_free | User2 part in ROM, free size

## Get system log download page

- URInterface: http://$ReceiverIpAddress/httpapi.asp?command=getsyslog
- Description: No use? But you can go to http://$ReceiverIpAddress/data/sys.log to download the log. Fileformat is unknown.

- Supported Formats: non-json form value
- HTTP Request: GET
- Command: getsyslog
- Response:
```
	<!doctype html>
	<html>
		<head>
		    <meta charset="utf-8">
		</head>
		<body>
		    <DIV><span id="dl">&nbsp;&nbsp;&nbsp;&nbsp;<a href=data/sys.log>download</a><hr></span></DIV>
		</body>
	</html>
```

## Network connection configuration WIFI
Get list of WIFI networks Available (SSID)

- URInterface: http://$ReceiverIpAddress/httpapi.asp?command=wlanGetApList
- Description:
List all wifi networks (SSID) identified by LinkPlay.

- Supported Formats: JSON
- HTTP Request: GET
- Command: wlanGetApListEx
- Response: (here 3 wifi networks)


	```{"Res": "0", "aplist": [
	{"Ssid": "wmmAudio_a7b8", "bssid": "00: 22: 6c: 00: a7: b8", "rssi"
	Th ":" OPEN "," encry ":" NONE "," extch ":" 1 "},
	(Ssid): "WIIMU_Network", "bssid": "20: dc: e6: cb: 7e: 78", "rssi"
	Th ":" WPA2PSK "," encry ":" AES "," extch ":" 0 "},
	{"Ssid": "WIFIAudio_29b0", "bssid": "00: 22: 6c: 16: 29: b0", "rssi": "65"
	Th ":" OPEN "," encry ":" NONE "," extch ":" 0 "}]}```


Description of fields:

Fields | Description
-------|----------------
res | Back to the list
Aplist | SSID List
Ssid | Wifi visible name, wlanGetApListEx returned ssid Hexadecimal encoding to support speciacharacters and the Chinese.
Bssid | Mac Address
Rssi | Signal Strength
channel | Wifi channel
auth | Encrypt
encry | Encryption Type
Extch | ?


## Wifi network connection
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=wlanConnectAp:ssid:channel:auth:encry
: Pwd: chext

- Description: Allows LinkPlay to be connected to a wifi network selected.

- Supported Formats: JSON
- HTTP Request: GET
- Command: WlanConnectApEx: SSID = xxx: ch = n: auth = xxx: encty = xxx: pwd = xxx: chext n =



Parameter | Mandatory? | Type | Description
----------|------------|------|---------------------
Ssid | True |  string | When connecting the wifi name ssid, wlanConnect ApEx, in hexadecimal code transmission
channel | True | string | Wifi channel to connect, optional 1-12
auth | True | string | Whether the encryption is OPEN or WPA2PSK
Encry | True | string | Encryption type, AES or NONE
Pwd | True | string | Password Wifi, type the password is OPEN NONE; When wlanConnect ApEx, when transmitting hexadecimacode, if the Password is empty, you do not have to enter.
Chext | True | string | 1 to fill

- Response:
Does not return any value, you must call the connection state of
The query interface, to determine if the connection was successful.


## Get SSID of current connected WiFi network
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=GetCurrentWirelessConnectEx

- Description:
Request the SSID of the WiFi the LinkPlay is connected to, SSID will be in hex

- Returns a non-json form value
- HTTP Request: GET
- Command: wlanGetConnectState
- Response: res:4D79535349444E616D65:1

Response '4D79535349444E616D65' has to be converted to ASCII 'MySSIDName'.
Value '1' is unknown.

## Connect to a hidden wifi network
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=wlanConnectHideApEx:ssid:pwd

- Description: Allows LinkPlay to be connected to a wifi network selected. The ssid and pwd must be in hexadecimal format.

- Supported Formats: JSON
- HTTP Request: GET
- Command: wlanConnectHideApEx: SSID: pwd

## State request for wifi connection
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=wlanGetConnectState

- Description:
Allows you to request the status of the LinkPlay wifi connection.

- Returns a non-json form value
- HTTP Request: GET
- Command: wlanGetConnectState
- Response: OK

Description of fields:

Field | Description
------| ------------
PROCESS | Liaison Process
PAIRFAIL | Password Error
FAIL | Error, then captured state then 10s continuously Captured, in order to ensure that this state is stable, otherwise it There may be only a temporary cut
OK | Connection is successful

## Hide or show SSID
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setHideSSID:1

- Description:
Allows you to request a SSID to be hidden or shown

- Returns a non-json form value
- HTTP Request: GET
- Command: setHideSSID:1
- Command: setHideSSID:0
- Response: OK

## Get built-in WiFi info
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getNetwork

- Description:
Allows you to request information about the built in AP

- Supported Formats: JSON
- HTTP Request: GET
- Command: getNetwork


Response:


	{
	  "securemode": "1",
	  "auth": "WPAPSKWPA2PSK",
	  "encry": "AES",
	  "psk": "wifipassword"
	}


Field | description
------|------------
securemode | unknown, maybe if authentication is enabled
auth | security protocol used for authentication
encry | encryption standard used for authentication
psk | encryption key for the network

# Music Player and Control
## Reading Status
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getPlayerStatus

Description: Allows you to query LinkPlay to find out: The currently playing song, the title of the song and other metadata

- Supported Formats: JSON
- HTTP Request: GET
- Command: getPlayerStatus
Response:


	{
		"Type": "0",
		"Ch": "0",
		"Mode": "10", "
		"Loop": "0", "
		"Status": "play",
		"Curpos": "12900",
		"Totlen": "229000",
		"Title": "736865",
		"Artist": "47726f6f766520436f766572616765",
		"Album": "xxxxxxxxxx",
		"Plicount": "1",
		"Plicurr": "1",
		"Flight": "90",
		"Mute": "0",
	}


Field | description
------|------------
type | 0: Normal Main speaker Loudspeaker 1: Sub-Speakers
ch | Channel 0 indicates stereo, 1 left channel, 2 of the right channel
mode | Playback Mode<br>PLAYER_MODE_NONE 0<br>PLAYER_MODE_AIRPLAY 1<br>PLAYER_MODE_DLNA 2<br>PLAYER_MODE_WIIMU 10<br>PLAYER_MODE_WIIMU_LOCAL 11<br>PLAYER_MODE_WIIMU_STATION 12<br>PLAYER_MODE_WIIMU_RADIO 13<br>PLAYER_MODE_WIIMU_SONGLIST 14<br>PLAYER_MODE_WIIMU_MAX 19<br>PLAYER_MODE_HTTP 20<br>PLAYER_MODE_HTTP_LOCAL 21<br>PLAYER_MODE_HTTP_MAX 29<br>PLAYER_MODE_ALARM 30<br>PLAYER_MODE_LINEIN 40<br>PLAYER_MODE_BT 41<br>PLAYER_MODE_EXT_LOCAL 42<br>PLAYER_MODE_OPTICAL 43<br>PLAYER_MODE_LINEIN_MAX 49<br>PLAYER_MODE_MIRROR 50<br>PLAYER_MODE_TALK 60<br>PLAYER_MODE_SLAVE 99
loop | Song playback modes playlist: 0: 1 play order: Single Cycle 2: Random Playback 3: List Cycle
eq | The current equalizer settings
status | Current status: play, load, stop, pause
curpos |  Current location, in milliseconds
totlen | The total length, in milliseconds
Title | Title, hexadecimal code, the name of the song; unknown if The song name displays the file name or the display unknown
Artist | Hexadecimal coding of artists
Album | Album name, hexadecimal encoding
plicount | The total number of playlists
plicurr | The current track of the playlist index
vol | Current volume
mute | Is currently muted



## Playing a Playlist
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:playlist:uri:<index>

- Description: Allows you to play a playlist with an extension index

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd: playlist: uri: <index>
- Response: OK

## Pause / resume playing the current music
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:pause


http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:onepause


http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:resume

- Description: Controls the player. <br>pause: pause current playback<br>resume: resume playback<br>onepause: if you pause in the resume, if playback is paused

- Supported Formats: none
- HTTP Request: GET
Controls:
- setPlayerCmd: pause
- setPlayerCmd: onepause
- setPlayerCmd: resume
- Response: OK



## Playing music
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:play:<URI>

- Description: Starts playback of a file after one
Pause

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd: play:<URI>
- Response: OK

## Previous song playback
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:prev

- Description: Allows you to play back a previous song

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd:prev
- Response: OK

## Play next track
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:next

- Description: Allows you to play back the next song

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd:next
- Response: OK


## Fast forward and rewind
URInterface:
Http://10.10.254/httpapi.asp?command=setPlayerCmd:seek:position

- Description: Allows you to play back or fast-forward one
piece

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd:seek:position
- Response: OK

## Stopping playback
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:stop

- Description: Stops the current playback

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd:stop
- Response: OK


## Adjusting volume
URInterface:
Http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:vol:value

- Description: Adjusting the volume of the player, the value is one volume value of 0-100. Speakers will also change the volume Main and under loudspeaker

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd:vol:value
- Response: OK


## Mute mode
URInterface:
`http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:mute:1`

- Description: Activation of the Mute mode, according to the following parameter Activation = 1 and Deactivation = 0

- Supported Formats: none
- HTTP Request: GET
- Command: setPlayerCmd:mute:1
- Response: OK

## Set the playback mode
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:loopmode:0

- Description: Starts different playback mode.<br>Available modes:
<br>0 Reading in order<br>1 Continuous playback<br>2 Shuffle playback<br>-1 Continuous play of a song

- Supported Formats: none
- HTTP Request: SET
- Command: setPlayerCmd:loopmode:0
- Response: OK



## Adjusting the Equalizer Mode
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:equalizer:mode

- Description: Adjusts the equalizer.<br>Available options:<br>0 Close Equalizer Mode<br>1 Classic Mode<br>2 mode Popular<br>3 mode Jazzy<br>4 Vocal Mode

- Supported Formats: none
- HTTP Request: SET
- Command: setPlayerCmd: equalizer: mode
- Response: OK

## Viewing Equalizer Mode
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getEqualizer

- Description: Allows to interrogate the mode device Equalizer in Progress

- Supported Formats: none
- HTTP Request: GET
- Command: getEqualizer
- Response: Mode 0/1/2/3/4  (See modes explained in previous paragraf (set) )

# Playback Control  MicroSD Card

## Viewing the File List
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getLocalPlayList

- Description: Get a list of music files on the Disk, the list of network files to return the results

- Supported Formats: JSON
- HTTP Request: GET
- Command: getLocalPlayList

Response:

	{
		"Num": "2",
		"Locallist": [
			{
				"File": "/ media / sda1 / avrilavigne - tik tok.mp3"
			},
			{
				"File": "/ media / sda1 / Aprilavigne - hush hush.mp3"
			}

		]
	}

Description of fields:

Field | Description
------|------------
Num | Number of files
locallist | List of files available on disk
file | File path (hexadecimal encoding)



## Get file information
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getFileInfo:index:range

- Description: Allows to obtain the detailed information of each of the files, on the basis of the index of each one in the list and from 0. (metadata in hexadecimal encoding).
- Supported Formats: JSON
- HTTP Request: GET
- Command: getFileInfo:index:range

Response:
If num is greater than 1, the file info returned is multiple.

	{"Num": "2", "infolist": [{
	"Filename": "/ media / sda1 / avrilavigne - hush hush.mp3",
	"Totlen": "0",
	"Title": "unknown",
	"Artist": "unknown",
	"Album": "unknown"
	},
	{
	"Filename": "/ media / sda1 / avrilavigne - hush hush2.mp3",
	"Totlen": "0",
	"Title": "unknown",
	"Artist": "unknown",
	"Album": "unknown"
	}]}


If num is less than 1, the file info return is unique;

	{
	"Filename": "/ media / sda1 / avrilavigne - hush hush.mp3",
	"Totlen": "0",
	"Title": "unknown",
	"Artist": "unknown",
	"Album": "unknown"
	}




Description of fields:

Field | Description
-----|------------
filename | File name (hexadecimal encoding)
totlen | Always returns "0"
Title | Song title or unknown (hexadecimacoding)
Artist | Artist of the song or unknown (hexadecimacoding)
Album | Album of the song or unknown (hexadecimacoding)

## Playing an Audio File on MicroSD
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:playLocalList:index

- Description: Allows you to select a file based on the
getLocalPlayList playlists, playing songs automatically.

- HTTP Request: GET
- Command: setPlayerCmd:playLocalList:index

## Get a list of cached files
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getCacheList

- Description: Provides a list of cached files

- Supported Formats: JSON
- HTTP Request: GET
- Command: getCacheList

Response:

	{
	"Num": "2",
	"Cachelist": [
	{
	"File": "/ media / sda1 / avrilavigne - tik tok.mp3"
	},
	{
	"File": "/ media / sda1 / Aprilavigne - hush hush.mp3"
	}

	]
	}


Description of fields:


Field | Description
------|-------------
num | Number of files
cachelist | List of Cached Files
file | File path (hexadecimal encoding)

## Get information about cached files
URinterface
http://$ReceiverIpAddress/httpapi.asp?command=getCacheFileInfo:index:range

- Description: Allows to obtain the detailed information of
each of the files, on the basis of the index of each one in the list and from 0. (metadata in hexadecimal encoding).

- Supported Formats: JSON
- HTTP Request: GET
- Command: getCacheFileInfo:index:range

Response:
If num is greater than 1, the fileinfo returned is multiple.


	{"Num": "2", "infolist": [
	{
	"Filename": "/ media / sda1 / avrilavigne - hush hush.mp3",
	"Metadata": "unknown",
	},
	{
	"Filename": "/ media / sda1 / avrilavigne - hush hush2.mp3",
	"Metadata": "unknown",
	}]}

If num is  1, the fileinfo returned is single.

	{
	"Filename": "/ media / sda1 / avrilavigne - hush hush.mp3",
	"Metadata": "unknown",
	}


Description of fields:  

Field | Description
------|-------------
Filename | File name (hexadecimacoding)
Metadata | Song information or unknown (Hexadecimal encoding)




# Multi-Room Management

## Get a list of LinkPlay available
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:getSlaveList

- Description of the interface: Allows to obtain the list of the devices using the same communication protocol.

- Supported Formats: JSON
- HTTP Request: GET
- Command: Multiroom:getSlaveList

Response:

	{
	"Slaves": "1",
	"Slave_list": [
	{
	"Name": "FA5100_a3f4",
	"Mask": "0",
	"Volume": "90",
	"Mute": "0",
	"Channel": "0",
	"Ip": "10.10.10.100",
	"Version": "WIFIAudio.1.2.2321"
	}
	]
	}


Field | Description
------|-------------
Slaves | Number of LinkPlay available
Slave_list | Information about each Sonoé iEast case available
name | Name
mask | Case already in Multi-Room mode, Yes = 1, No = 0
Volume | Volume level
Mute | Enable Mute mode, Yes = 1, Off = 0
Channel |  Wifi channel
ip | IP address of the LinkPlay Boot
version | firmware version


## Removing a LinkPlay from the multi-room
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveKickout:ip

- Description of the interface: Allows to remove from the multiroom mode a device Based on its IP address.

- Supported Formats: None
- HTTP Request: GET
- Command: Multiroom: SlaveKickout: ip
- Response: OK

## Hide the IP address of a LinkPlay
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveMask:ip

- Description of the interface: Allows to integrate a multi-room mode a device Based on its IP address.
It is thus rendered invisible from the IP network.

- Supported Formats: None
- HTTP Request: GET
- Command: Multiroom:SlaveMask:ip
- Response: OK


## Releasing a Multi-Room Mode
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveUnMask:ip

- Description of the interface: Allows to release from the multi-room mode based on its IP address. It is thus visible on the IP network.

- Supported Formats: None
- HTTP Request: GET
- Command: Multiroom:SlaveUnMask:ip
- Response: OK



## Individual volume adjustment
URInterface: http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveVolume:ip:volume

- Description: Allows you to adjust the individual volume of the each of the devicees via the IP address of the device and the definition of a value going from from 1 to 100.
Note: these settings will be lost when deactivating multi-room mode (kickout)

- Supported Formats: None
- HTTP Request: GET
- Command: Multiroom:SlaveVolume:ip:volume
- Response: OK

## General Volume Adjustment
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:slave_vol:volume

- Description: Adjusts the overal volume of the multi-room with the definition of a value ranging from 1 to 100.
Note: thesis settings will be lost When disabling multi-room mode

- HTTP Request: GET
- Command: setPlayerCmd:slave_vol:volume
- Response: OK


## Individual activation Mute
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveMute:ip:mute

- Description: Enables the Mute on each device via the IP address of the device and by enabling (1) and
disabling (0)

- Supported formats: None
- HTTP Request: GET
- Command: Multiroom: SlaveMute:ip:mute
- Response: OK

## General activation Mute
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:slave_mute:mute

- Description: Enables the muting

- HTTP Request: GET
- Command: setPlayerCmd: slave_mute: mute
- Response: OK  

## General Mute Disabling
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:slave_mute:unmute

- Description: To disable the mute mode so overal
the
- Supported formats: None
- HTTP Request: GET
- Command: setPlayerCmd:slave_mute:unmute
- Response: OK


## Individual management of the audio signal Right / left
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveChannel:ip:channel

- Description: Enables the Mute on Each of the devices via the IP address of the device and by this parameter to signal right only Channe0 = left and only 1 = Channel signal

- HTTP Request: GET
- Command: Multiroom:SlaveChannel:ip:channel
- Response: OK

## Overal management of the audio signal Right / left
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:slave_channel:channel

- Description: Enables the Mute on Each of devices via the IP address of the device and by this parameter to signal
right only Channel= 0 and left signal only 1 = Channel

- HTTP Request: GET
- Command: setPlayerCmd:slave_channel:channel
- Response: OK

## Individual definition of the device Name
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:SlaveSetDeviceName:%ip:%s

- Description: individual settings of the name of the square in mode UPnP / Airplay

- HTTP Request: GET
- Command: Multiroom: SlaveSetDeviceName: ip%:%s
- Response: OK




## Disabling Multi-Room
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=multiroom:Ungroup

- Description: Disables the multi-room mode

- HTTP Request: GET
- Command: Multiroom : Ungroup
- Response: OK


# Control parameter network

## Opening the WPS server
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=wpsservermode

- Description: Opening of WPS standby server integration of new device

- HTTP Request: GET
- Command: wpsservermode
- Response: OK

## Closing the WPS server
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=wpscance

- Description: Opening of WPS standby server integration
of new devices

- HTTP Request: GET
- Command: wpscance
- Response:
unknown command

## WPS Client opening for device
URL:
http://$ReceiverIpAddress/httpapi.asp?command=wpsclientmode

- Description: WPS server to integrate opening a device

- HTTP Request: GET
- Command: wpsclientmode
- Response: OK


## Change the SSID name of the device
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setSSID:value

- Description: Sets a new network name (SSID) of the device in hexadecimaformats

- HTTP Request: GET
- Command: setSSID:value
- Response:
No response. The system restarts partner after the call.

## Setting the password WIFI
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setNetwork:1:password

- Description: Setting a new password using letters and / or numbers and crossing of setnetwork setting: 1 (Securing WIFI network (WPAPSK) in contrast, setnetwork: 0 (oPEN) Makes the network open WIFI.

- HTTP Request: GET
- Command: setnetwork: 1: password
- Response:
No response the system restarts after the validation of the new password.
password The Therefore must reconnect to the WiFi network and enter the new password.
password.


## Restoring the factory setting
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=restoreToDefault

- Description: To restore factory settings, erasing defined configurations. The device restarts.

- Supported Formats: No
HTTP  Request: GET
- Command: restoreToDefault
the response back:
OK

## Restarting the device
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=reboot

- Description: Allows you to reboot the device

- Supported Formats: None
- HTTP Request: GET
- Command: reboot
- Response: OK

## Programming stop device (switching off)
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=setShutdown:sec

- Description: Used to turn off the device timed.

- HTTP Request: GET
- Command: setShutdown:sec
- Response: OK

## Show time left to shut down
URInterface:
http://$ReceiverIpAddress/httpapi.asp?command=getShutdown

- Description: Shows the current information about time left to shut down (in seconds)

- HTTP Request: GET
- Command: getShutdown
- Response: number (in seconds)


## Stop WIFI signa
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPowerWifiDown

- Description: Turns off the WIFI signadevice

- HTTP Request: GET
- Command: setPowerWifiDown
- Response: OK


## Setting the MCU display

the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=MCUDisplayText:xxxx

- Description: Manage a MCU text display in the limit of 32 characters.
-
- Supported Formats: None
- HTTP Request: GET
- Command: MCUDisplayText:xxxx
- Response: OK

## Setting the name of device
URL
http://$ReceiverIpAddress/httpapi.asp?command=setDeviceName:%s

- Description: Sets the name UPnP, DLNA and Airplay of the device (Hex)

- HTTP Request: GET
- Command: setDeviceName:%s
- Response: OK

# Firmware Update

## Update search
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=getMvRemoteUpdateStartCheck

- Description: Search for the firmware updates available

- Supported Formats: No
- HTTP  Request: GET
- Command: getMvRemoteUpdateStartCheck
- Response: OK

## Update availability
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=getMvRemoteUpdateStatus

 - Description: Allows you to check if an update is available. May need to call Severatimes Because The device Itself need to query the server if updates are available.

- Supported Formats: No
- HTTP Request: GET
- Command: getMvRemoteUpdateStatus

Response:

Value | Meaning
------|----------------------
40 | Improved package
10 | Being Analyzed
others | update Refusal


## Notification updates
URL:
http://$ReceiverIpAddress/httpapi.asp?command=getMvRemoteUpdateStart

- Description: After calling the interface, if a new version is available, the device starts to download updates. At the
end of the download, the update process starts. <br>WARNING: DO NOT POWER OFF DURING THIS PROCESS!!

- Supported Formats: No
- HTTP Request: GET
- Command: getMvRemoteUpdateStart
- Response: OK

## Status of the update process
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=getMvRemoteUpdateStatus

- Description: Get the download progress.

- Supported formats: None
- HTTP Request: GET
- Command: getMvRemoteUpdateStart
- Response:

Value | Meaning
------| --------
10 | Under review
21 | The verification of the downloaded update file failed
22 | Downloading the update file failed
23 | The verification of the downloaded update file failed
25 | Start downloading
27 | Download complete
30 | Downloading and verification completed


## Download progress
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=getMvRomBurnPrecent

- Description: Status of updating

- Supported Formats: None
- HTTP Request: GET
- Command: getMvRemoteUpdateStart

Response:


	
	{
	" status ":" 0 "," progress ":" 50 "
	}



Fields | Meaning
---------| --------------------------
status  | State
progress | Progress between 0 to 100%



# Clock and Timer
## Time synchronization
If the device is online, the device using the system time synchronization SNTP, Taking Time UTC, so if there is not UTC, for example, Paris is GMT+ 8, the appellant must be converted to UTC, Then calsetAlarmClock.

If the device is online, you can use to adjust the system time:

http://$ReceiverIpAddress/httpapi.asp?command=timeSync:YYYYMMDDHHMMSS

## Set the timer
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setAlarmClock:n:trig:op:time[:day][:url]

- Description: [?] Hooks que la indicates field is required, for example, is set to trip at a daily alarm instruction

http://$ReceiverIpAddress/httpapi.asp?command=setAlarmClock:n:trig:op:time:url

?

- HTTP Request : GET
- Command: setAlarmClock: n: trig: op: time [: day] [: url]

Fields | Description
-------|-------------------
not | Can be from 0 to 2, Max 3 alarms
trig | Trigger mode:<br>0 - No alarm (setAlarmClock: n: 0)<br>1 Once only<br>2 Daily<br>3 Weekly<br>4 Weekly, Extended Mode<br>5 All month
op | Action to take<br>0 - Running the script<br>1 - Playing music<br>2 - Stop playback
time | Format %% 02h 02m 02s%<br>Such as 180101 for 6:01:01 pm<br>start time: 00-23<br>minutes and seconds 00 to 59
day | Format% 04M% 02s% 02J (M: month / s week / d: day)<br>For example 20,140,101, qui est 01 months assignment to 12<br>Mode Only once - no setting can<br>mode Everyday - No feasible setting<br>mode every week -<br>value of 00 -06 (2 bytes) - 00 Sunday 06 Saturday day.<br>mode Weekly, extended mode<br>The first byte Represents the specific day of the value of triggering actions (0 Sunday to Saturday 6). if ee is set to 1 (ie, Attributed To 7F) indicates que le input<br>power of a day. Note must be two bytes between 1 and 31. If the trigger once, Then set% 04d% 02d% 02d, for example 20,140,101, qui est 01 months to 12 assignment
url | localize the script maximum length of 256 bytes

## Remaining playing time (Timer)
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=getAlarmClock:n

Field | Description
-------|-------------------------
n | Can be from 0 to 2, Max 3 alarms. <br>Defined: return { "enable": "1"}<br>Undefined: return { "enable": "0"}
trigger |"%d"
operatio | "%d"
Time | Format% 02h% 02m% 02s<br>mode Just ounce - "Date": "% 02d:% 02d:% 02d" or no <br>mode Every week (extended mode included) - "WEEK_DAY": "%d"<br>mode Every day - "day" "% 02d "" time ":"% 02d: 02d:% 02d "
path | "%s"


## Off alarm

the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=alarmStop

- Description: Stop Programmed alarm

- Supported formats: None
- HTTP  Request: GET
- Command: alarmStop
- Response: OK

# Source Line IN
## Read Access Line IN
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=setPlayerCmd:switchmode:%s

- Description: Access to the different reading mode as possible in the qui Line In.
line-in : Switch to AUX mode,
optical : Go SPDIF mode
UDISK : Go to the Micro SD reader
wifi : GB WIFI mode

- HTTP Request: GET
- Command: setPlayerCmd:switchmode:%s
- Response: OK



# Simulation Instruction IO
## Instruction GPIO pullup
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=IOSimuPullUp:%d

- Description: Allows management of the GPIO

- 0: nReload not recommended, Generally used for WPS and factory reset
- 11: GPIO_nReady (only A02)
- 12: GPIO_DCD
- 14: GPIO_RIN
- 18: GPIO1 (only A11)
- 17: GPIO2 (only A11)
- Command: IOSimuPullUp:%d

## Instruction pulldown GPIO
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=IOSimuPullDown:%d

- Description: Delete GPIO management forced
- Command: IOSimuPullDown:%d

## GPIO reading
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=IOSimuRead:%d

- Description: Read GPIO
- Command: IOSimuRead:%d

## Analog controlkey input
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=IOSimuKeyIn:%d

- Description: References MCU settings. The MCU MCU Receives instruction + XXX KEY +

- Command: IOSimuKeyIn:%d

## Analog controlkey output
the URinterface:
http://$ReceiverIpAddress/httpapi.asp?command=IOSimuKeyOut:%d

- Description: References MCU settings. The MCU Receives instruction AXX + KEY + XXX Voice
- Command:
the URinterface:<br>http://$ReceiverIpAddress/httpapi.asp?command=PromptEnable<br>
http://$ReceiverIpAddress/httpapi.asp?command=PromptDisable

Description:
- Command: PromptEnable and PromptDisable
