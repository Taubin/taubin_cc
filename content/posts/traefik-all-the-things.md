+++
categories = ["Traefik", "Blog", "Server", "HomeServer"]
date = 2020-01-09T11:00:00Z
description = ""
draft = false
featureImage = "https://static.taubin.cc/img/photo-1584949091598-c31daaaa4aa9_.jpg"
thumbnail = "https://static.taubin.cc/img/photo-1584949091598-c31daaaa4aa9_.jpg"
slug = "traefik-all-the-things"
tags = ["Traefik", "Blog", "Server", "HomeServer"]
title = "Traefik All the Things"
+++


If you followed my [Containerize All the Things](../../../../2019/06/25/containerize-all-the-things/index.html) post, you know I’ve moved my entire home server workflow to Docker. There were a few reasons for this, but most of all because it made it incredibly easy to move everything or have everything backed up in case of a catastrophic failure of some sort. After all, my hard drives are quite old and have been running hard out.

![](https://static.taubin.cc/2020-01-10/drive_age.jpg)

Old drives

For a long time, I used NGINX as a reverse proxy. There’s nothing really wrong with that, but I do love to experiment from time to time on new things. One of the things I’ve heard quite a bit about is Traefik. It’s listed on the [website](https://containo.us/traefik/) as “The Cloud Native Edge Router”. In other words, a reverse-proxy.

If you go to their website, you’ll see the usual corporate BS about how great it is, how many companies use it, etc… The one thing that really intrigued me about it, is the simple integration with Docker. I use Docker for almost everything these days (as pointed out above) and being able to have the proxy automatically pick it up and serve everything, taking care of my SSL certs was great. So I started out learning more.

The first place I always start out with learning new things, is the official docks, if there are some. Luckily for me, there are: [docs.traefik.io](https://docs.traefik.io/) I started out there, and read through everything. It had some easy to follow examples and I used them to test everything out. Unfortunately, I ran into some minor issues.

I use Cloudflare for all of my DNS. There are a couple of reasons, however it being free and quite reliable is near the top of the list. The one small issue with that, is that I also use LetEncrypt for all of my certificates. That’s not _really_ a problem, but can make things a little more difficult. Since I use Cloudflare, getting a wildcard certificate (for example \*.taubin.cc) to use for my domain can get a little complex. I have to use a DNS resolver for the certificates instead of just an HTTP resolver.

I ran into some issues getting things working properly with the wildcart cert, as traefik wasn’t asking cloudflare properly for the certificate. I ended up asking for help on reddit, and getting quite a bit of help with it. I was able to get it functioning in the end, and below is a (somewhat redacted) copy of how I made things work.

<script src="https://gist.github.com/Taubin/8729e095b6f195d9ef6ed81955633c77.js"></script>

That’s long I know, and it works (for the most part). The one issue I’ve run into is trying to get it working properly with the ciphersuites.

A helpful person on reddit suggested I define everything as a command instead of using the toml file. This was an amazing suggestion and has actually made things a bit better. I’m still experimenting, however, this does seem to be working. The only problem I’ve run into so far, is I’ve run afoul of Lets Encrypt’s rate limiting. That will solve itself in time though.

For now, below is the (currently being worked on) traefik docker-compose file I’m using. I still have a lot to add, like hardening up the TLS certificate handling, but for now it’s working properly.

<script src="https://gist.github.com/Taubin/062a0cbcabd3bd5f3886947b061b5007.js"></script>

I’ll be updating this post as things progress, but for now, this seems to be a working function of Traefik with Cloudflare and Lets Encrypt wildcard certificates.



