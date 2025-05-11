---
title: "Otsi -  PCB rev1"
date: 2025-01-03
draft: false
description: "First revision of PCB's for Otsi mk2"
---

### Design
The first idea was to create something like a handheld so that one could use Otsi everywhere. But there are a few issues with this approach. First of all, it's getting pretty big pretty quickly and our goal was to make it as cheap to build as possible. That means fitting within JLCPCB's 100x100mm size for the cheapest PCB. And that's the first issue with this design. They didn't fit within those dimensions by like 5mm so 5 PCBs. And, with delivery and taxes, it cost us almost 20 bucks. Enough of a back story, here is what we came up with as rev1.

{{< image src="galleries/galleryOL1/3&2_v3.png" alt="alter-text" position="center" command="fill">}}

Being completely honest. We are proud of those PCBs bc beside the dimension issue they look good, and work... most of the time...

### First issue (check your schematics 4 times...)
Here you have our schematic for this PCB and let's play a little game. Look at it and try to figure out what is wrong with it, connection wise.

{{< image src="galleries/galleryOL1/schematic1.png" alt="alter-text" position="center" command="fill">}}

So in this version two V regulators are placed so that Pico with displays is powered from one and ICs from the other one. First voltage regulator is connected to +3V3 line and the second one to +3.3VP line...

{{< image src="galleries/galleryOL1/schematicError.png" alt="alter-text" position="center" command="fill">}}

and that's the problem. The regulator is connected to +3V3 line but everything else to +3.3V. And we didn't catch it earlier bc of using 2 voltage regulators, Pico and displays had power so we completely forgot about the difference in voltage regulators. This one tiny mistake led us to buying an oscilloscope and investigating if the capacitance of I2C lines is correct... That being said, always remember to check your schematic and measure voltage at the beginning. And before our next problem, let's look at the assembled PCBs

### Semi-soldered PCBs
After receiving our package with PCBs we made another mistake, we have soldered everything (or almost everything at once)

{{< image src="galleries/galleryOL1/semi_v1.png" alt="alter-text" position="center" command="fill">}}

Soldering everything at once is a big problem bc you don't know what exactly is causing errors and have to desolder everything piece by piece. And the second thing we should have done is using gold pins sockets for e.g. Pico instead of soldering it directly. It would have saved us a lot of trouble later.

### I<sup>2</sup>C addressing issues
Another thing to keep in mind is checking all of your I<sup>2</sup>C devices beforehand. We didn't do it bc we thought that it would take too much time, where, in fact, it would save some. Our problem was that 2 of the devices had the same address and everything connected to the BUS after those devices were working only when you jumped on one leg around it and didn't breath near them for exactly 2.3s or saying it normally, they just were working randomly. And after We figured this out, there was one last problem.

### Never mess with config files for Arduino
We are using a [library](https://github.com/earlephilhower/arduino-pico) for programming Pico in Arduino IDE. And after a stroke of genius someone (Simon...) has changed something in config files and bc of it none of the I2C devices were working properly. They just didn't communicate with Pico... We have spent 1 whole week debugging it every day... It was a pain...

### Last words
This project log is slowly coming to an end but We hope you have learned that rushing stuff never helps and that your stupidity is your biggest enemy. See you in the next Otsi update.

##### Stay creative and slow down  
##### ~Otsi development team

<br/>
{{< button label="Return" link="/projects/otsi.mk2/otsi-info/" style="solid" >}}













