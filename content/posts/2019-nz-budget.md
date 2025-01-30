+++
categories = ["NZ", "New Zealand"]
date = 2019-05-28T12:00:00Z
description = ""
draft = false
featureImage = "https://static.taubin.cc/img/photo-1459257831348-f0cdd359235f_.jpg"
slug = "2019-nz-budget"
tags = ["NZ", "New Zealand"]
title = "2019 NZ Budget"
thumbnail = "https://static.taubin.cc/img/photo-1459257831348-f0cdd359235f_.jpg"
+++


There has been a whole lot happening here in NZ in the past 24 or so hours. You see the 2019 budget for NZ is meant to be released tomorrow (Thursday), but was apparently leaked by the opposition party on Tuesday. This has led to a lot of speculation, name calling, threats, police reports, etc… You know typical politics.

Now normally I wouldn’t care about this at all, and certainly wouldn’t write about it here. The thing is, anyone that knows me knows I don’t really care for politics. I never discuss it and don’t follow any of the parties. That said I do vote, but not even my wife knows (or cares) who I vote for.

Why am I writing about this now and here then? Well it’s because of the amount of misinformation around this subject. There are articles like [this one on Stuff NZ](https://www.stuff.co.nz/business/113082731/budget-hack-theory-could-raise-questions-as-to-what-is-illegal) that state it was all just a guess that allowed the people that provided the leak to National to download the budget. This simply is not true. Anyone that’s developed websites knows that any time you are linking to a document on a webpage, it is usually not stored on the same server as the webpage. Instead it’s usually stored on a CDN or a file server.

If we take a look at [said webpage](https://web.archive.org/web/20190528090806/https://treasury.govt.nz/publications/glance/budget-glance-2019), it simply shows a [403](https://en.wikipedia.org/wiki/HTTP_403) error. The link provided here is a cached copy of the webpage, as it will certainly change after Thursday’s official release of the budget. Many organizations both large and small, will set up a placeholder page for an item that is going to be released at a soon date. Case in point is this one. The webpage is set up as a placeholder, and a 403 status code is given to it.

This allows search engines to start to parse the page prior to it being actually enabled, and also allows a very fast set up of the page once it’s ready for release. I can even give you an example of this right here on this page. If you click the link below, it will take you to a pdf of a leaked budget for my household. That’s right, this wasn’t going to be released until Friday, but I’m giving you a leaked version right here!

If you click on [THIS LINK](__GHOST_URL__/super-secret-budget-page/) it will take you to a leaked version of my budget for 2019.

![](https://static.taubin.cc/2019-05-29/leet-haxxor.webp)

A totes legit haxxor
Photo by [NeONBRAND](https://unsplash.com/photos/_Kmtj6UIlGo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/hacker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Now let’s break this down like a leet haxxor would. At least the type that are referred to by the likes of Stuff. We can see that the page exists on this web server. It’s linked right there to taubin.cc. So that totally means the super secret page exists! So far so good. There’s even a link there to my super secret budget.

Let’s have a look at that. If you hover over the link, or even open it you’ll see that the link points to a subdomain of taubin.cc. Strange, why would that be. Using our leet haxxor skillz, we can assume a few things. Either that is a random coincidence, or it’s just to keep things easy and means nothing. Unfortunately, our leet haxxor skillz are wrong. The correct answer is that the file is actually on a completely different server than the one this blog is hosted on. In fact that file happens to be on my CDN (Content Delivery Network). In fact if you look at any of the images on this blog, they are all hosted on my CDN, and not on the same page (or even server) that they appear.

Taking this as an example, we can see how the Treasury department of New Zealand does things. They have a website set up, most likely on a dedicated server, and host the actual files on another server. This means they can set up a webpage prior to uploading the actual files (in this case PDF files), on their public file server. So you see, it’s entirely possible to have a link to a webpage, with something on that webpage without it actually linking to the budget document.

This is precisely what has happened here. They have created the webpage (just like they have for previous years) following the same naming schema as they have in past years (because that’s the way to do things properly), and left the link to the actual document out of it until it’s ready for public publishing.

### So what has actually happened?

Well, we can make a few assumptions based on what we’ve been told. First the National Party stated on Tuesday that they had [received a copy](https://www.stuff.co.nz/national/politics/113051412/govt-to-spend-13-billion-on-defence-nats-claim-govts-budget-details-leaked?rm=a) of the budget prior to it’s official release on Thursday. The Finance Minister stated he has [informed the police](https://www.stuff.co.nz/national/politics/113077002/budget-leak-referred-to-police-after-treasury-finds-evidence-of-hacking) that their servers have been hacked after they found evidence of said hacking. This started a whole lot of speculation.

A user on twitter stated the information was [publicly available](https://web.archive.org/web/20190529034251/https:/twitter.com/norightturnnz/status/1133305324796952576) at the link provided above. He initially stated this information was out in the public view and not actually “hacked”. He was proven incorrect as the webpage only showed the 403 page listed above, with no actual link to the PDF containing the budget. This of course hasn’t stopped the media from taking this and running with it. However as we’ve proven on this post, the PDF would not have been posted directly on the same web server as the web page is.

After all of that happened the leader of the National Party, Simon Bridges, came out and said National had [done nothing wrong](https://web.archive.org/web/20190529034835/https:/twitter.com/simonjbridges/status/1133292488511197186) while accusing the head of the Treasury of smearing his party. The problem with this is that the Treasury is pretty impartial when it comes to politics. They don’t answer to either party. He has since doubled down on this, and stated they aren’t doing anything wrong by possessing the information and releasing it.

The problem with this, is that it is in fact illegal. However that again is not the point here. To get back to the known facts:

*   The budget was never posted on the Treasury website
*   The Treasury was in fact hacked
*   Police are investigating

Based upon that, there’s a whole lot of misinformation going around right now unfortunately. We won’t know what really happened for quite a while (if ever) but we can see how this misinformation about the PDF of the budget being publicly accessible on the website is simply incorrect. Hopefully this helps clear stuff up from a technical standpoint if nothing else.

Before believing everything the media (social and otherwise) tells you, try to look into the way those things work first, and make your own opinion. I’m not here to sway it, I’m simply here to help understand how it works from a technical standpoint.



