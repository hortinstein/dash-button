![Blank Dash](http://i.imgur.com/PP0CJ3s.png?1)
# node-dash-button
[![gitter](https://img.shields.io/badge/GITTER-join%20chat-green.svg?style=flat-square)](https://gitter.im/hortinstein/node-dash-button)

Place it. *Hack it.* Press it. ~~Get it.~~

This module was inspired by [this fantastic article by Edward Bensen](https://medium.com/@edwardbenson/how-i-hacked-amazon-s-5-wifi-button-to-track-baby-data-794214b0bdd8).

It is a simple library that will allow you to utilize a dash button to emit an event.  I am using the same strategy of watching for dash generated ARP requests as the article above.

### Contents
-----------------
- [Installation Instructions](#installation-instructions)
- [First Time Dash Setup](#first-time-dash-setup)
- [Find a Dash](#find-a-dash)
- [Example Usage](#example-usage)
- [To do](#to-do)
- [License](#license)

#### Installation Instructions
The following should work for ubuntu, the main thing for any os is getting the libpcap dependancy.
``` sh
# dependancy on libpcap for reading packets
$ sudo apt-get install libpcap-dev
$ npm install node-dash-button
```
#### First Time Dash Setup

Follow Amazon's instructions to configure your button to send messages when you push them but not actually order anything. When you get a Dash button, Amazon gives you a list of setup instructions to get going. Just follow this list of instructions, but don’t complete the final step (#3 I think) **Do not select a product, just exit the app**.

#### Find a Dash
To find a dash on your network, run the following from the node-dash-button directory in node_modules:
``` sh
# you may need to use sudo due to libpcap running in permiscuous mode
$ cd node_modules/node-dash-button
$ node bin/findbutton
```

It will watch for new arp requests on your network.  There may be several arp requests, so press it a few times to make sure. Copy the hardware address as shown below

![hw address](http://i.imgur.com/BngokPC.png)

#### Example Usage:
``` js
//warning this may trigger multiple times for one press
//...usually triggers twice based on testing for each press
var dash_button = require('node-dash-button');
var _ = require('lodash');
var dash = dash_button("8f:3f:20:33:54:44"); //address from step above
var found = function() {
    console.log("omg found");
};

dash.on("detected", _.debounce(found, 20000, true));
```

#### To do
- API revisions (look at accepting a list and emmitting mac address...cleaner)

#### License

The MIT License (MIT)

Copyright (c) 2015 Alex Hortin

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
