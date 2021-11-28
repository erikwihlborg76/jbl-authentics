# How to control a JBL Authentics speaker?

## What works

Using the [jbl-authentics node-red implementation](jbl-authentics.flow) you can:
* Change volume
* Set source to DLNA (to use Spotify) or to optical

### Web request examples:

| Command | URL |
| --- | --- |
| Volume up  | `GET http://node-red-host:1880/jbl/volume/up`|
| Volume down |  `GET http://node-red-host:1880/jbl/volume/down`|
| Source optical  |  `GET http://node-red-host:1880/jbl/source/optical`|
| Source DLNA (incl Spotify)  | `GET http://node-red-host:1880/jbl/source/dlna`|
| Source current | `GET http://node-red-host:1880/jbl/source/current`| 


## About the Node-RED implementation

### Invoke the flow using HTTP or an emulated Roku device 

While functionality can be accessed using web requests, you can also use the `node-red-contrib-fakeroku` as a simple way to integrate the node-red flow to `Logitech Harmony Smart control` or similar.

### What you must change to make it work

#### ☑️ Change JBL device hostname

The code makes use of `node-red-contrib-dnsquery` to translate the JBL Authentics device's hostname to an IP number. The code assumes the JBL device has this hostname `JBL-L8`. you can set a custom hostname for the device by logging in to the device's web UI (port 80).

#### ☑️ Change Emulated Roku IP address

Click the `fakeroku`node, located its configuration, and set `LAN IP`to the IP where you run node-red.


### Code quality is poor - but it works

The quality of the node-red flow is quite crappy, but it shows how to interact with a JBL Authentics device. This is a work in progress - parts of it does not work - for example, commands related to "power"


# Problem background & additional reading

## JBL Authentics devices can't easily be integrated into your smart home setup

**JBL Authentics L8** (and probably **JBL Authentics L16**) are speaker systems with support for Optical, Spotify, Airplay, and some more. The problem is that they lack documented ways to change source and volume.

While you could use [JBL Music](https://play.google.com/store/apps/details?id=com.harman.jblmusicflow) to control the device, it's not very convenient. 

## The "HK API" is similar to the API used to control JBL Authentics devices

JBL Authentics devices can be controlled over bluetooth and TCP - but none of the APIs are documented.

The TCP API is similar to an API used on Harman receivers. The API is sometimes referred to as "HK API". Here are links to more info about that API: 
* https://github.com/KarimGeiger/HKAPI
* https://things.adamparsons.id.au/hk-avr-151-remote-control-api/
* https://www.home-assistant.io/integrations/harman_kardon_avr/
* https://community.home-assistant.io/t/harmon-kardon-avr/7567/31
* https://github.com/Raidok/Raidok.github.io/blob/master/_drafts/node-red-harman-kardon.md




