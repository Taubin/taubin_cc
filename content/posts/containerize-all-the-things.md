+++
categories = ["HomeServer"]
date = 2019-06-24T12:00:00Z
description = ""
draft = false
featureImage = "https://static.taubin.cc/img/photo-1576124344805-c47cea66b0db_.jpg"
thumbnail = "https://static.taubin.cc/img/photo-1576124344805-c47cea66b0db_.jpg"
slug = "containerize-all-the-things"
tags = ["HomeServer"]
title = "Containerize All the Things"
+++


For quite a while, our house has used a server to host all of our media as well as some other items. There are a great many advantages to this, as it allows easy control over our movies, TV, music, comics, eBooks etc… Ever since the server was first built (it’s actually my old computer), it has run Windows 10 pro. There is nothing implicitly wrong with this, however Windows can be quite a resource hog. Just having it sit at the desktop, without much else running uses a couple of gigs of ram, as well as a bit of power to push the desktop even though it’s not actually being used.

I’ve been wanting to change this set up for quite a while, but I’ve not really had the push to do it. One of the reasons is the potential for downtime, which goes against wife approval standards. An easy way to do deal with this, would to be to containerize everything, then move it. But really, how much fun would that be? Things were chugging along happily until one day when the power went out. This is drastic for us, as at the time we didn’t have a way to get into our garage. Upon everything coming back up, a portion of my Windows partition had corrupted itself. Now this can happen to any OS, but it was the push I needed.

* * *

Ubuntu to the rescue!

Instead of recreating everything within Windows, I decided to move everything to one of the most popular linux distros available Ubuntu.

I’ve been running Ubuntu on all of my web servers for as long as I can remember. It’s pretty easy to learn once you really dive into it, and there is a lot of community support for it. After formatting my main SSD drive in the server, I downloaded the [Ubuntu 18.10 Server image torrent](https://ubuntu.com/download/alternative-downloads#bittorrent). That’s right kids, torrents can be used for good as well as evil!

After Ubuntu server was installed, I got started mounting my drives (more on that later) and installing Docker. Things are about to get technical, so if you aren’t interested, skip past this point section.

Technical bits
--------------

I first had to find the drive partitioning for my drives other than the main drive where Ubuntu was installed. In order to do so, I SSH’d into the server (using just my ssh keys, security kids! no passwords here!), and ran the following to get a mapping of my drives:

    sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL

* * *

![](https://static.taubin.cc/2019-06-25/drives.PNG)

I love the new Windows Shell!

This showed my my currently installed drives, and their drive paths. Here you can see there are 3 drives installed, the 125 gig SSD as the main drive, a 3 TB drive and a 4 TB drive. When I initially did the installation, the 4TB drive was actually in an external NAS enclosure made by WD. It’s quite old and I had difficulty with some of my docker containers using it properly, so I ended up shucking it and installing it directly.

Once I knew where the drives were within Ubuntu (SDA and SDB), I was able to make a directory for each, give the directories permission, and map the drives in /etc/environment

    sudo nano /etc/fstab

    ## Drive mounts:
    #D drive mount - Red drive - 4 TB
    /dev/sda        /media/d        ext4    defaults        0       2
    #E drive mount - Old Drive 3 TB
    /dev/sdb        /media/e        ext4    defaults        0       2

* * *

Once the drives were mounted and verified, I started the set up of Docker and Docker-Compose. I first ran the usual linux updates (apt update && apt upgrade -y) then got to the installation.

* * *

    # Update
    sudo apt-get update

    # Install certificates for adding the docker key
    sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg-agent \
        software-properties-common

    # Install docker key
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

    # Add docker repo
    sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"

    # Update apt
    sudo apt-get update

    # Install Docker
    sudo apt-get install docker-ce docker-ce-cli containerd.io

    # Download docker-compose
    sudo curl -L https://github.com/docker/compose/releases/download/1.24.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

    # Make it executable
    sudo chmod +x /usr/local/bin/docker-compose

    # Add myself to the docker group
    sudo usermod -aG docker ${USER}

    # Set up my environment so I don't need to keep adding the usergroups and timezone
    sudo nano /etc/environment

    PUID=1000
    PGID=999
    TZ="Pacific/Auckland"

* * *

That’s it! The technical bits done (for the most part).

![](https://static.taubin.cc/2019-06-25/guillaume-bolduc-uBe2mknURG4-unsplash.webp)

Photo by [Guillaume Bolduc](https://unsplash.com/@guibolduc?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Once the hard part was done, installing Docker, Docker-Compose and setting all the directories and permissions, I was good to go. All I needed to do was put together my docker-compose file and run it.

The great thing about Docker is everything is held into little containers. Each of them are separated from each other, so if one breaks, it’s not going to bring down the entire system. This can have it’s many advantages, as well as some disadvantages. Luckily for me, the advantages are greater than the disadvantages.

One of the greatest advantages to this system, is being able to keep all of the data used by the containers (TV, Movies, etc…) completely separated from the container, and simply added as a volume. This means if I ever need to replace my main drive, or rebuild the system for whatever reason, I can simply remap my volumes, and run my docker-compose file and be right back where I left off. Another great advantage is this system uses much fewer resources than my windows box did.

![](https://static.taubin.cc/2019-06-25/htop.PNG)

htop showing the currently used resources

With 20 running containers, my server is happily chugging along with 2 gigs of ram in use, and barely any processor usage. Something that would be practically impossible with Windows 10. Even this blog is being run on the server currently (as I write it that is, it’s hosted on a webserver). Needless t
