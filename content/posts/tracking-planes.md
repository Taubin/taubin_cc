+++
categories = ["RTL-SDR", "Planes"]
date = 2019-01-07T11:00:00Z
description = ""
draft = false
featureImage = "https://static.taubin.cc/img/photo-1515446808777-87f69cb475aa_.jpg"
thumbnail = "https://static.taubin.cc/img/photo-1515446808777-87f69cb475aa_.jpg"
slug = "tracking-planes"
tags = ["RTL-SDR", "Planes"]
title = "Tracking Planes"
+++


Tracking some planes 🛩️ using an SDR and homemade antenna
----------------------------------------------------------

Over Christmas this past season, I spent quite a bit of time with my in-laws. While down there my father in law mentioned he was having issues getting his RTL-SDR dongle to work properly on his new laptop, and asked if I could help. For those not aware, RTL-SDR stands for RTL Software Defined Radio. They have been extremely popular for a long time for not only pulling in analog TV signals, but also tracking planes.

Most planes transmit their signal in near real time, by using the ADS-B [Automatic dependent surveillance – broadcast](https://en.wikipedia.org/wiki/Automatic_dependent_surveillance_%E2%80%93_broadcast) signalling system. This allows not only other planes, but also ground control, ATC and other see where the planes are, what direction and speed they are headed, and a lot of other information. All of these signals are transmitted at 1090mhz. Luckily for us, someone has figured out how to read these signals using a cheap tv dongle.

Both my father in law and myself have used these dongles for a couple of years to track planes. He is on limited bandwidth with his internet, however I’m lucky enough to not be so I also transmit this data to various trackers around the world. Unfortunately for my father in law, his tracker was not working properly with his new Acer laptop. We tried a number of times to get it working properly, however the software he was using to receive these images, was not allowing the dongle to power up properly. We have found a solution, but that’s not the point of this post, so I’ll spare you.

![A typical SDR dongle](//static.taubin.cc/rtl-sdr.jpg)

Helping him work out his issues with the laptop and his SDR dongle to track planes (which he does without an internet connection) renewed an interest in me in not only tracking planes, but seeing what else can be done with one of these amazing little dongles. When you purchase most dongles, they come with a basic antenna made for pulling analog tv stations. Because of this, they are not ideal for pulling 1090 signals. You will get some, however there are much better ways.

I had initially purchased an antenna from Amazon that was supposedly tuned for 1090. I had also purchased a slightly more expensive dongle which included a built in filter to help filter out other signals. Using this I had decent reception and was feeding the data to Flight Radar 24. I knew however, there had to be a better way.

My father in law mentioned a [coaxial collinear antenna](https://www.balarad.net/) he had seen, and thought it would be fun to build while I was down there. We went to his garage and found the coax we needed, as well as the connectors needed to hook the antenna up to a dongle, and went to work. Well, I’ll be honest, he did all the work. He cut it to proper lengths, trimmed the insulation and pressed the coax into lengths. Once it was all put together, he placed the entire thing in a PVC enclosure, and we plopped it up on his roof to test it out.

He is in a nice location with very open skies, and the ability to place his antenna directly at the peak of his roof. Talk about ideal! Once we had the antenna in place, we immediately started to pull in data. He was pulling data from approximately 220 nautical miles away. This is exceptional performance from a home built antenna made out of nothing other than some coax!

![My CCA attached to my window (not an ideal location)](https://static.taubin.cc/cca.jpg)

Once the antenna was tested and verified, he gave it to me to take home, which was super generous of him. He stated he will probably make himself another antenna in the future that can be tossed into the back of his car, and used at the airport nearby. When I finally arrived home, I tacked it up in the best place I have at this time, taped to my window. Using this, I’ve been able to increase my distance as well as number of reported planes by a lot. I now feed to nearly every source I can find, and have been experimenting.

The data that gets streamed to the various flight tracking sites, looks like this in it’s json format:

        { "now" : 1546903703.3,
      "messages" : 266783,
      "aircraft" : [
        {"hex":"3a65a2","category":"A0","version":0,"mlat":[],"tisb":[],"messages":254,"seen":94.5,"rssi":-33.9},
        {"hex":"c8221c","flight":"GBA590  ","alt_baro":2325,"alt_geom":2675,"gs":154.6,"tas":166,"track":216.1,"roll":1.1,"baro_rate":-576,"squawk":"6412","category":"A1","nav_qnh":1019.0,"nav_altitude":1504,"nav_modes":["vnav"],"lat":-36.837982,"lon":174.867897,"nic":6,"rc":926,"seen_pos":1.4,"version":1,"nic_baro":1,"nac_p":7,"nac_v":0,"sil":3,"sil_type":"unknown","mlat":[],"tisb":[],"messages":1645,"seen":1.4,"rssi":-32.9},
        {"hex":"c817bd","category":"A1","version":2,"sil_type":"perhour","mlat":[],"tisb":[],"messages":746,"seen":97.3,"rssi":-35.1}
      ]

Luckily there is an easier way to look at the data using the same platform that creates the data, dump1090. Dump1090-fa (the version I’m using on my pi) creates a really useful website to present the data locally to you. You can see an example of it below, while it tracks an airplane that happened to be passing by.

![Dump 1090 locally hosted page](//static.taubin.cc/dump1090.png)

I’m also able to pull some stats from my dump1090 client, which is written to an external hard drive in order to save writes to my sd card on my raspberry pi. You can view my stats so far below. Not bad for a little over a week!

![Dump 1090 aircraft distance in nautical miles](//static.taubin.cc/distance.svg)

![Dump 1090 featureImageage from my antenna](//static.taubin.cc/featureImageage-nmi.svg)

![Dump 1090 hourly messages sent](//static.taubin.cc/messages-hourly.svg)

You can certainly look forward to hearing more about my adventures in SDR, I’m planning on becoming a HAM, as well as tracking some satellites and pulling data from them. In fact, I just pulled my first decent weather image today off of NOAA 18. Until next time!

Edit: I’ve since moved the antenna outside to my wife’s planter. I’m hoping it stays stable and will keep an eye on it. I’m also wondering how long it will be before my apartment manager contacts us to take it down, even though it’s not attached to anything…



