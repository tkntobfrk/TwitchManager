# About
This software manages notifications from twitch chat, awards in stream currency, monitors twitter and displays tweets in stream.  All of this is intended to be self contained within docker containers. As a base this should allow users to cusomize the bot without much technical knowledge.

# Setup
- Download [Docker Toolbox](https://www.docker.com/products/docker-toolbox)
- Get twitch auth tokens [Twitch Apps](https://twitchapps.com/tmi/) - required
- Get twitter auth tokens [Twitter Apps](https://apps.twitter.com/) - required
- Get Google Api key [Google Developer console](https://console.developers.google.com/) - optional

# Configure
- Launch Docker Quickstart Terminal
- git clone https://github.com/tkntobfrk/TwitchManager.git

# Configure Twitch Chat
- update twitch.json with twitch auth tokens
- update twitchWhisper.json with twitch auth tokens

# Configure Twitter search
- update twitter.json with twitter auth tokens
- update twitter.json with search term(s), can be comma seperated

# Configure Google Calendar - optional
- update calendarCtrl in controllers.js with api tokens googleCalendarApiKey
- get the share value of the calendar you'd like to share and add to controller on googleCalendarId

# Configure IP - maybe
- depending on how you setup Docker Toolbox change to /app/services/services.js may be needed
- In docker toolbox execute docker-machine ip default
- this IP must match /app/service/services.js
```javascript
appServices.factory('socket', function ($rootScope) {
    var socket = io.connect('http://192.168.99.100:8000');
    console.log('connected to socket');
```

# Configure commands.json
- Users can add commands as necessary, !debit & !credit should remain static
- This is generally a work in progress but basic commands should work fine if added with restict: none, value: whatever needs to be said, and name: !mycommand or !whatevercommand
```json    
	{
        "name": "!mycommand",
        "description": "This is my command",
        "restrict": "none",
        "type": "info",
        "value": "This will be chatted!!"
    },
```

# Run the bot
- cd TwitchManager
- docker rm -f $(docker ps -a -q)
- docker rmi $(docker images -q)
- docker-compose up -d

# Use bot notifications
- point clr or streaming browser items at http://192.168.99.100:8000/index.html
- Note if you have a different docker ip the ip above should be changed to that value
- IP can be found by issuing docker-machine ip default within docker quickstart terminal

# Use bot calendar
- point clr or streaming browser items at http://192.168.99.100:8000/calendar.html
- calendar can be shared amongst users stream teams can setup a shared schedule
- work inprogress

![alt text](https://cloud.githubusercontent.com/assets/4344301/13550807/76332fa8-e2eb-11e5-8135-33e55a481e9d.PNG)

# Use timer
- point clr or streaming browser items at http://192.168.99.100:8000/timer.html
- in chat type !timer add $num_minutes

# TwitchManager
- Need anti spam for commands, maybe use expiring keys, to avoid api block
- levels for display of user points in chat

# Twitch chat bot V2
- UI to configure timer display
- UI to configure bot commands
- redis interface for account
- giveaways

# Cleanup
- create tutorial for api keys (calendar, twitter, twitch)
- create video tutorial for misc setup

# Twitter enhancements
- wire up the tweet command
- check webrtc to twitter?
