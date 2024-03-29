# Ingress Hubot

A collection of Ingress-related commands for Hubot. This script is designed
specifically for use with the Slack adapter.

[![Build Status](https://travis-ci.org/hubot-scripts/hubot-ingress.svg)](https://travis-ci.org/hubot-scripts/hubot-ingress)

## Features

* Report level requirements
* List requirements for all levels
* Store badge information for players
* Calculate recharge rate and max distance for AP level
* Calculate septicycle/checkpoint times
* *much more to come...*

## Installation

`npm install hubot-ingress`

Then add `"hubot-ingress"` to `external-scripts.json`

Go to the custom emojis page of your Slack team. Upload each of the images from
the `badges/` subfolder, naming them the same as their filename (without the extension).
These emoji will be used by Hubot.

## Configuration

`HUBOT_GOOGLE_GEOCODE_KEY` - An optional Google Geocoding API key. 
If configured, this will be used by the "intelmap" feature in order to 
convert an address to a lat/long for the intelmap link. The intelmap link 
generator should function without this, but it may be needed if the 
intelmap generator begins returing no results at some point. 

A Geocoding API key can be obtained easily from the [Google Developer Console](https://console.developers.google.com). 
At the time of this writing, 2,500 requests/day are provided for free. 
Create a new project for your hubot in the developer console, unless you 
have one already. Enable "Geocoding API" under "_APIs_" and then 
create a new key under "_Credentials_".

`HUBOT_CYCLE_TIME_FMT` - Optionally ovveride the display format for times (see Moment-timezone.js). Default is "ddd hA" (e.g. "Sun 10pm")

`HUBOT_CYCLE_TZ_NAME` - Optionally set the timezone name (e.g. 'EST' see Moment-timezone.js). This wins when set.

`HUBOT_CYCLE_TZ_OFFSET` - Optionally set the timezone offset (e.g. '-05:00', see Moment.js). Defaults to the server instance's offset. This is used when `HUBOT_CYCLE_TZ_NAME` is not provided.

## Commands

### AP requirement

Reports the AP/badge requirements for the specified level.

`hubot AP until L<level>`

### List levels

Show the AP/badge requirements for every level.

`hubot AP all`

### Add badges

Badges can be added one by one or multiples at a time, and can be added for other players.
Badges that have levels end with a number representing that level (1=bronze, 2=silver, etc).
When a badge is added that is the same as an existing badge (hacker5 vs hacker1, for example),
then the new badge will replace the existing badge.

`hubot I have the hacker3, founder badges`

`hubot user1 has the recursion badge`

### Remove badges

Badges can be removed one by one.

`hubot I don't have the hacker1 badge`

### Get Intel map

Gives you a link to the Ingress Intel map based on Google Maps search.

`hubot intelmap soho ny`

### Calculate max recharge distance

Calculate maximum distance from which an agent can recharge, based on agent level.

`hubot recharge distance [level]`

### Calculate recharge rate/percentage

Calculate recharge efficiency for an agent, based on agent level and distance.

`hubot recharge rate [level] [distance]`

Note: The distance parameter defaults to km, but it can also convert imperial units, e.g. `hubot recharge rate 11 450 miles`

### Get Septicycle times

Calculate the next septicycle start. Optionally provide a number X to get the next X start times.

`hubot septicycle|cycle [count]`

### Get Checkpoint times

Calculate the next checkpoint start. Optionally provide a number X to get the next X start times.

`hubot checkpoint|cp [count]`

### Get Timezone Offset

Returns the current configured timezone offset.

`hubot cycle offset`

### Set Timezone Offset

Set the timezone offset. See [Moment.js](http://momentjs.com/docs/#/manipulating/timezone-offset/) for how to configure this.

`hubot cycle set offset [offset]`
