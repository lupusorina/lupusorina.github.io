---
layout: post
title:  loose connectors
date:   2024-07-24 13:39:00
description: connectors
tags: robotics electrical_engineering biped
---


One of the main challenges I've faced with connectors for my biped's motors is preventing them from being under excessive tension.
As the robot moves its legs, significant mechanical stress can be applied to these connectors, and if this stress is not properly managed, the connectors can become loose over time.

To illustrate this, I have two GIFs: one showing a connector without proper mechanical stress relief and one where the stress relief was implemented properly. 

<div class="row justify-content-sm-center">
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/2024-07-24/IMG_0658.mp4" title="loose connection" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/2024-07-24/IMG_0664.mp4" title="tight connection" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
Loose connection vs. tight connection for the XT30 connector on the MJBots motor controller.
</div>

One issue arising from unstable power supplies is the potential for voltage drops or spikes on the CANbus.
This can lead to many problems, including motor drivers breaking.
For example, one of my MJBots motor driver recently signaled Fault 33, indicating a likely malfunction.
According to the [documentation](https://github.com/mjbots/moteus/blob/main/docs/reference.md), it means: "the most common reason for this is undervoltage, moteus attempted to draw more current than the supply could provide."
MJBots provides really nice tech support on their Discord channels, so according to them: "That indicates damage to the gate driver or fets or both". I ordered a new motor driver, which just arrived, so I'll solder it real quick.

Meanwhile, I've asked one of my summer students, Cesar, to design a mount to be able to attach the cables more securely.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/2024-07-24/mounts.jpeg" title="mounts" class="img-fluid rounded z-depth-1" %}
    </div>
</div>







