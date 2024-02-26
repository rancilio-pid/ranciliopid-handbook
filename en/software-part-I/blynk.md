---
layout: default
title: Blynk setup
parent: Software Part I
grand_parent: EN - Manual
has_children: false
nav_order: 2
---

# Einrichtung von Blynk
{: .no_toc }

Contents

* TOC
{:toc}

## Introduction

The next step is to set up the Blynk app on your phone to be able to control the PID parameters. Blynk is a cloud service which makes NodeMCU controllable from your phone or tablet. We have our own Blynk server available which is hosted by Markus. You can of course also use the public Blynk server but probably have to deal with additonal costs for setup etc.


The principle workflow is as follows:

The PID in your machine sends data to the Blynk server where the app can access it as well. Communication is in both directions, meaning the Blynk server not only receives data from the PID for visualization purposes etc. but also provides configuration data to the PID. To make sure only you can access your machine, an Auth token is used.

Markus has a video on Youtube which explains the installation procedure


## Video: Installation and setup of Blynk app

[![Installation video](https://img.youtube.com/vi/JHDRUN044gQ/hqdefault.jpg)](https://www.youtube.com/watch?v=JHDRUN044gQ)

## Step 1: Download and install app

from the app store on your phone

## Step 2: create account

Open the Blynk app and click „Create New Account“

![](../../img/software-part-I/blynk/IMG_0115-576x1024.png)

click on the traffic-light symbol to change the server!
Otherwise you will use the "normal" Blynk server

![](../../img/software-part-I/blynk/IMG_0116-576x1024.png)

**Important**:

Switch to „Custom“.
Server address: blynk.remoteapp.de
Port: 9443
confirm with „OK“

![](../../img/software-part-I/blynk/IMG_0117-576x1024.png)

add your email address and click next

![](../../img/software-part-I/blynk/IMG_0119-576x1024.png)

Your account has now been created
Create your first project by clicking "New Project"

Here, you can also direcly press the "scan" symbol an scan the following QR code:


QR-Code for Android:

![](../../img/software-part-I/blynk/qr_android_v292.png)

QR-Code for IOS:

![](../../img/software-part-I/blynk/qr-ios.jpg)

(shown PID values are not up to date!)

![](../../img/software-part-I/blynk/pid-werte.gif)

or create the app yourself.

![](../../img/software-part-I/blynk/IMG_0120-576x1024.png)

Give the project a meaningful name, choose "NodeMCU" as device

![](../../img/software-part-I/blynk/IMG_0121-576x1024.png)

To read the AuthKey (will be needed in Arduino IDE), press the square in the upper right corner


![](../../img/software-part-I/blynk/IMG_0124-576x1024.png)

Now, press the "nuts" symbol

![](../../img/software-part-I/blynk/IMG_0123-576x1024.png)

The AUth code is shown in the lower part of the screen, it is basically the key for encrypting the communication between NodeMCU, the server and your phone and should be kept sectet. You can also email it to yourself.


![](../../img/software-part-I/blynk/IMG_0122-576x1024.png)



## Step 3: integrate Auth token into program code

The Authkey will be written into userConfig.h in the variable AUTH, SSID and PASS will be the name and password for your Wifi network. More on that in Part 2
