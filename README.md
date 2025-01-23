# интеркосмос keyboard
My experience modifying and building a 34 key ferris sweep keyboard I themed after the Soviet-US space race...

## Synopsis
### [The Original Repo]() - please reference
### Parts List

Item | Notes | Amount | Total Cost
---|---|---|--:
<a href="">PCB Fabricator</a>|Other vendors also work...|5 (minimum order size- use 2)|$12
<a href="">Jade switches</a>|Choose whichever switch you like the feel of most- get a sample of a bunch if necessary, as this board is NOT hot-swappable. |34|$20
<a href="">Keycaps</a>|Keycaps with letters go in and out of stock often, and are more expensive.|34|$12-$35
<a href="">Elite-C V4</a>|Any microcontroller with this footprint works. I recommend USB C mc's, and look for bluetooth if you want a wireless keyboard.|2|$40 
<a href="">USB-C Cable</a>|You want data and power, but it doesn't have to handle much of either.||$8
<a href="">TRRS Jacks</a>|...|2|$1
<a href="">TRRS Cable</a>|...|1|$4

### Hardware
- Soldering Iron
- Tweezers [optional]
- Multimeter (not strictly, but VERY useful for checking electric continuity- if a key doesn't work, you can identify whether the issue is in the software, the pcb, the MC or switch pads, or the switch) [optional]
- Rosin (I didn't use any, but makes the microcontroller far easier to solder) [optional]
### Software
- KiCad
- QMK (command line, qmk toolbox, VIAL, et cetera- use what tools you need)
- Text editor or IDE [semi-optional]
- Adobe Illustrator (or a FOSS alternative) [optional]
### Skills
- 

# Process

## Inspiration
[Ben Vallack]() made a number of incredible videos on the ferris sweep (and it was his earlier videos reviewing the [gergoplex]() and [moonlander]() keyboards that led me to being interested in split keyboards and owning a moonlander myself, respectively). This linked one was vital to my problem solving and process, but I recommend checking out his other videos.



## Tools



## Design

![](https://raw.githubusercontent.com/mindcat/media_repository/main/spacerace/initialdes.png)
![](https://raw.githubusercontent.com/mindcat/media_repository/main/spacerace/finaldes.png)
![](https://raw.githubusercontent.com/mindcat/media_repository/main/spacerace/finalexp.png)

## Build

![](https://raw.githubusercontent.com/mindcat/media_repository/main/spacerace/build1.png)
![](https://raw.githubusercontent.com/mindcat/media_repository/main/spacerace/build2.png)
![](https://raw.githubusercontent.com/mindcat/media_repository/main/spacerace/build3.png)

## Software

Nothing unexpected if you're familiar with using [QMK](https://docs.qmk.fm/newbs) to make keymaps, though I'm sure all the GUI tools would work fine as well. 

## [OPTIONAL] 3D Printed Case

A couple weeks of knocking the keyboard halves around in my bag led me to designing a pretty simple clamshell 3D printed case for it. Layered on top of each other, the keyboard is ~32 mm thick. Edge to edge (lengthwise) it is ~120 mm wide. The first print was (as a factor of speed, carelessness, and limited experience with Fusion360) designed very imprecisely- working solely of those prior two measurements and a screenshot of the copper layer and edgecuts from KiCAD. 

Luckily, after printing it way too large the first time, I have a well printed and reliable case that I still don't use nearly enough. Unplugging the halves is minor, but somehow enough to discourage me from doing anything more than just putting the keyboard in a side pocket of my bag- especially since the case adds some cm that stop it from fitting in most convenient pockets in a bookbag. The Fusion files, as well as stls (v2 for FDM, v1), are included regardless...
