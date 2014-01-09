node-samsung-airconditioner
===========================

A node.js module to interface with Samsung SMART Airconditioners

Install
-------

    npm install samsung-airconditioner

API
---

### Load

    var API = require('samsung-airconditioner').API;


### Discover

    new API().on('discover', function(aircon) {
      // now login!
    }).on('error', function(err) {
      console.log('discovery error: ' + err.message);
    });

### Login

      // if the caller already has a token associated with aircon.props.duid, then supply it, else null

      aircon.login(token, function(err, token) {
        if (!!err) return console.log('login error: ' + err.message);

        // remember token for next time!

        // now drive the aircon!
      }).on('waiting', function() {
        console.log('please power on the device within the next 30 seconds');
      }).on('end', function() {
        console.log('aircon disconnected');
      }).on('err', function(err) {
        console.log('aircon error: ' + err.message);
      });

#### Drive the aircon after logging in

    aircon.onoff(true);

    aircon.mode(type);                   // one of 'auto', 'cool', 'dry', 'wind', or 'heat'

    aircon.set_temperature(celcius);
    aircon.get_temperature(function(err, celcius) {});

    aircon.set_convenient_mode(mode);    // one of 'off', 'quiet', 'sleep', 'smart', 'softcool', 'turbomode',
                                         // 'windmode1', 'windmode2', 'windmode3'

    aircon.sleep_mode(hours);
