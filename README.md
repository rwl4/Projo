# Projo

A server and mobile web app I made to control my video projector without a
remote.

My current setup is a [Benq
W1070](http://www.benq.com/product/projector/w1070/) projector that is linked to
a [TP-Link TL-MR3020](http://wiki.openwrt.org/toh/tp-link/tl-mr3020) wireless device via
a RS-232 cable. A 12V trigger cable has been wired between the projector and
the motorized screen so the screen is now automatically controlled by the
projector (no more remote either).

This devices delivers a RESTful webservice to interface to the video
projector via serial commands (Crestron protocol) and a web app that I use
on my mobile devices to replace the remote.

I made it to fit my own needs but it should pretty much work out of the box for
other devices (any \*nix running computer with a RS232 connector) and the
Crestron protocol seems to be common to multiple brand of AV equipement.

## Software

 * OS: [OpenWRT](https://openwrt.org)
 * Web Server: [Flask](http://flask.pocoo.org)
 * Web App: [AngularJS](http://angularjs.org)

[Bonjour](http://en.wikipedia.org/wiki/Bonjour_(software)) is used for
auto-discovery so I just need to go the `http://projo.local` on my mobile
devices and optionnaly add the App to the Home Screen.

Once launched there is a few buttons on the top and bottom. The dark area in
the center is a gesture interface to the menu. Swipe left/right/up/down
navigate in the menu, a tap select an item, a double tap goes back one level.

AngularJS has been selected because I needed an excuse to play with it. It's used
in conjunction with [CoffeeScript](http://coffeescript.org), [Yeoman](http://yeoman.io), [Grunt](http://gruntjs.com) and [Bower](http://bower.io).

## Hardware

![Serial cable on projector below ceiling...](http://farm3.staticflickr.com/2890/9703297446_a1c43fa01d_c.jpg)

![...that goes upstairs to the
device](http://farm8.staticflickr.com/7391/9703298054_edb5deed06_c.jpg)

![TTL to RS232 board and wiring](http://farm4.staticflickr.com/3674/9700287609_4cc2cd62fa_c.jpg)

The base block is a TP-Link TL-MR3020 router. I selected it for the following
reasons: it's cheap, runs OpenWRT, has UART pins readily accessible, enough
(albeit barely)
room inside to fit the serial board and did I mention it's cheap? 

It's comparable in price to the Raspberry Pi but comes with wifi, internal
storage, a case and a power supply. And the Raspberry Pi would be overpowered
for that task.

Only drawback is that the internal storage is just 4MB so a USB drive had to be added for my
needs.

The board is a simple [MAX232](http://en.wikipedia.org/wiki/MAX232) based TTL
to RS232 adaptater. The UART on the router works a 3.3V so the MAX232 converts
it to signals compatible with other RS232 devices. You can find them on ebay
for a penance by searching for "TTL to RS232".

Wiring is simple: 

* 5V from the router goes to the 5V pin on the board
* Ground from the router goes to the ground pin on the board
* RX on the router goes to TX on the board
* TX on the router goes to RX on the board

And that's pretty much it, drilling the holes in the case took longer.

Here is the pinout on the router: [MR3020 pins](http://wiki.openwrt.org/_detail/media/tp-link_mr3020_top-pcb-gpio-pins.jpg?id=toh%3Atp-link%3Atl-mr3020).
I did add a 10K pullup resistor between VCC and TX as recommended on the
documentation but I'm not sure if it's necessary.

Do note that you'll need a straight DB9<->DB9 male-female cable (or you'll
spend a few days wondering why it doesn't work with a null-modem cable).

## Installation

Here is a detailled [installation guide](INSTALL.md) that covers the setup needed to get it
up and running.
