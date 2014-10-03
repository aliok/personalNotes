---
layout: post
title:  "RaspberryPi Notes"
date:   2014-10-03 20:45:15
categories: public
---

### Console cable :
<https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable/overview>

#### Console cable driver installation:
<http://changux.co/osx-installer-to-pl2303-serial-usb-on-osx-lio/>

#### Check if it is available using:
{% highlight bash %}
> kextstat -b nl.bjaelectronics.driver.PL2303
Index Refs Address            Size       Wired      Name (Version) <Linked Against>
  227    0 0xffffff7f828d3000 0xb000     0xb000     nl.bjaelectronics.driver.PL2303 (1.0.0d1) <116 34 5 4 3>
{% endhighlight %}

#### Connect:
`screen /dev/cu.PL2303-00001004 115200`

Username is : pi


### WiFi:
It cannot connect to hidden network easily.
I needed to do `sudo wpa_gui` and then `sudo iwlist wlan0 scan essid NETWORKSSID` to make it connect to hidden NETWORKSSID network.