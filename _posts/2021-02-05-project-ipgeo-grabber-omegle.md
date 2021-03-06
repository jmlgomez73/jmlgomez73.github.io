---
layout: single
title: '<span class="projects">IPGeo Grabber Omegle - Project</span>'
excerpt: "This script allows to obtain the geolocation of the stranger in a video chat on the Omegle platform in real time through the capture of the public IP, thanks to the Peer-to-Peer communication with WebRTC that follows the web."
date: 2021-02-05
categories:
  - projects
tags:  
  - javascript
  - webrtc
  - omegle
toc: true
toc_label: "Content"
toc_sticky: true
show_time: true
---

This script allows to obtain the geolocation of the stranger in a video chat on the Omegle platform in real time through the capture of the public IP, thanks to the Peer-to-Peer communication with WebRTC that follows the web.

## [Link to the Github repository](https://github.com/jmlgomez73/IPGeo-Grabber-Omegle)

# **LEGAL NOTICE AND DISCLAIMER**.
IPGeo Grabber Omegle is a script for the sole purpose of educational and research purposes for developers or end users, and may help create countermeasures for current threats.
I assume **NO** responsibility for how you choose to use any of the executables/source code of any files provided.

## Design and Purpose.

## Purpose

This script is intended in an informative way to show the ease by which the public IP of anyone using this platform can be obtained by using a **VPN** as a primary countermeasure while using this platform.

## Design, Implementation and Usage

This script uses **WebRTC** technology which allows us to communicate with another user in your web browser.

<a href="/assets/images/project-ipgeo-grabber-omegle/1.png">
    <img src="/assets/images/project-ipgeo-grabber-omegle/1.png" alt="ip geo grabber omegle">
</a>
<p align="center">WebRTC</p>

So we will employ the ```RTCPeerConnection`` API which allows us to open, maintain and close a connection with another person in Omegle, when we get an *Ice Candidate* (**ICE** = Interactive Connectivity Establishment, which allows two computers to talk to each other directly (**Peer-to-Peer**)) what we are looking for is to parse the information associated with it by dumping it into an array.

<a href="/assets/images/project-ipgeo-grabber-omegle/2.png">
    <img src="/assets/images/project-ipgeo-grabber-omegle/2.png" alt="ip geo grabber omegle">
</a>
<p align="center">ICE Candidates</p>

Where we will focus will be on the UDP candidates of type ```srflx``` (Server Reflexive Candidate) which are those generated by the **STUN** server which returns the ip address, port, status of the connectivity with the other person..., for this case we will simply get the public address of the other person.

<a href="/assets/images/project-ipgeo-grabber-omegle/3.jpg">
    <img src="/assets/images/project-ipgeo-grabber-omegle/3.jpg" alt="ip geo grabber omegle">
</a>
<p align="center">WebRTC, STUN/TURN Server</p>>

Later we will obtain the geolocation through the web *IpGeolocation.io* through requests using its API, for this we will need an *API-Key* which we can obtain by simply registering in its page.

We parse the server response to *JSON* and format the information we want, finally displaying it by console.

<a href="/assets/images/project-ipgeo-grabber-omegle/4.png">
    <img src="/assets/images/project-ipgeo-grabber-omegle/4.png" alt="ip geo grabber omegle">
</a>
<p align="center">Results</p>

## Usage

* On PC: In *Chrome/Opera/Mozilla*, in "Settings" => "More Tools" => "Developer Tools" => "Developer Tools", with developer tools open, we access ```omegle.com````, and in the "Console" tab in the developer tools area, paste all the code and hit "Enter", Now anyone you connect with, you will be shown information from it (in real time).

* On Android: *Chrome*, Using usb debugging and Chrome's "Remote Devices" option we can inject this javascript code remotely in our device's browser.

Follow this tutorial: <https://developers.google.com/web/tools/chrome-devtools/remote-debugging?hl=es>