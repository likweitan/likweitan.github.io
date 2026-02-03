---
date: "2020-02-17T21:45:24+08:00"
draft: false
title: "How to host a Minecraft server"
tags:
  - minecraft
---

# Verify that the latest version of Java is installed Java

Open a command window and enter the command java -version. If a version number is reported, then check the Java website to see what the most recent version number is.

```
C:> java -version
java version "1.8.0_241"
Java(TM) SE Runtime Environment (build 1.8.0_241-b07)
Java HotSpot(TM) 64-Bit Server VM (build 25.241-b07, mixed mode)
```

> If Java isn't installed or the version is outdated, download it from [here](http://www.java.com/download/).

# Starting the Minecraft Server

## Download the Server Pack

- [Download Now](https://drive.google.com/drive/folders/1sO24ZxtmBTujj-7qh7HH01qnVszcRc2o?usp=sharing)

> After downloading, place all files in the same folder.

## Open `start.bat`

![Step 1](https://i.ibb.co/YRW1VMf/Capture1.jpg)

> Wait for the latest version to download.

![Step 2](https://i.ibb.co/8P81GdT/Capture2.jpg)

> Once the download is complete, the process will stop automatically.

## Open `eula.txt`

![Open eula.txt](https://i.ibb.co/7SZCFSw/Capture3.jpg)

## Change `eula=false` to `eula=true`

Before:  
![Before](https://i.ibb.co/gPQ3th0/Capture4.jpg)

After:  
![After](https://i.ibb.co/89Chq0m/Capture5.jpg)

## Start the Server with `start.bat`

You can now access the server via `localhost`.

> Note: This is only for local network access.

# How to Find Your IP Address

## 1. Open the Command Prompt (cmd).

## 2. Enter `ipconfig`.

## 3. Look for the `IPv4 Address`—this is your local network IP.

In my case, the IP address is `172.18.140.51`, as shown below:

![IP Address](https://i.ibb.co/chn3tY8/ip.jpg)

# Configurations

Update later.

# References

[ServerJars - API](https://serverjars.com/updater)
