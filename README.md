# LICA

LICA is an open-hardware, open-source tensile robot that you can handcraft and accessorize to your liking. You can read more about the project in the [ACM T-HRI Paper](https://doi.org/10.1145/3310356) and in [Evan Ackerman's IEEE Spectrum article](https://spectrum.ieee.org/automaton/robotics/home-robots/blossom-a-creative-handmade-approach-to-social-robotics-from-cornell-and-google).

Here are two examples of LICA robots:

[![LICA robot bunny](https://camo.githubusercontent.com/aebf5852adfbe43717ad81d31c5654a25f79095d6360a595ee6fe3a191e6d398/687474703a2f2f677579686f66666d616e2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031372f30382f626c6f73736f6d2d62756e6e792d636f726e65722d65313530323831323137353733332d333030783138392e6a7067)](https://camo.githubusercontent.com/aebf5852adfbe43717ad81d31c5654a25f79095d6360a595ee6fe3a191e6d398/687474703a2f2f677579686f66666d616e2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031372f30382f626c6f73736f6d2d62756e6e792d636f726e65722d65313530323831323137353733332d333030783138392e6a7067) [![LICA robot jellyfish](https://camo.githubusercontent.com/6a10226b33275ae149be04a65d41428970c3a7917f5233e371c920099c673cca/687474703a2f2f677579686f66666d616e2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031372f30382f626c6f73736f6d2d6a656c6c79666973682d373638783630362e6a7067)](https://camo.githubusercontent.com/6a10226b33275ae149be04a65d41428970c3a7917f5233e371c920099c673cca/687474703a2f2f677579686f66666d616e2e636f6d2f77702d636f6e74656e742f75706c6f6164732f323031372f30382f626c6f73736f6d2d6a656c6c79666973682d373638783630362e6a7067)

**For any questions (assembly or software related), [please check/make public issues](https://github.com/maderdordor/LICA/issues).**

---

## How to Cite

If you use this repository or any of its content, please cite it as follows:

Michael Suguitan and Guy Hoffman. 2019. LICA: A Handcrafted Open-Source Robot. *J. Hum.-Robot Interact. 8*, 1, Article 2 (March 2019), 27 pages. <https://doi.org/10.1145/3310356>

Bibtex:

```
@article{suguitan2019lica,
author = {Suguitan, Michael and Hoffman, Guy},
title = {LICA: A Handcrafted Open-Source Robot},
year = {2019},
issue_date = {March 2019},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
volume = {8},
number = {1},
doi = {10.1145/3310356},
journal = {J. Hum.-Robot Interact.},
month = {mar},
articleno = {2},
numpages = {27},
keywords = {craft, social robotics, toolkit, handcrafted, robot toolkit, craft robotics,
            research platform, open-source, Robot design, soft robotics}
}
```

---

## LICA How-To

### Get repo

In a terminal, clone this repo

```bash
git clone https://github.com/maderdordor/LICA/
```

### Setup Software Dependencies

Make sure you're using [Python `3`]
To check, run `python -V` or `python3 -V`in the terminal to check the version. As of now, this codebase was tested and works on `Python 3.5.2` on Ubuntu 16.04 and Mac.

*The following steps will assume `python -V` reports with version `>3.x.x`. If it reports `2.x.x` then replace `python` in the following steps with `python3`*

Also ensure that [`pip3` is installed](https://pip.pypa.io/en/stable/installing/).
To install:

Ubuntu: `sudo apt install python3-pip`

Mac: `curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py`, then `python3 get-pip.py`

Virtual environments (`venv`) should be installed, but if not:

Ubuntu: `sudo apt-get install python3-venv`

Mac: `brew install python3-venv`

Make a `venv` (virtual environment) in the top `LICA` directory and activate it:

```bash
python -m venv lica_venv
source lica_venv/bin/activate
```

#### General Setup

*Ubuntu*: You may need to run

```bash
sudo apt-get install build-essential libssl-dev libffi-dev python3-dev
```

and

```bash
pip install wheel
```

To install dependencies, run in the main `LICA` directory:

```bash
pip install -r requirements.txt
```

*Mac OSX: You may need to append `--user` to the `pip` command to circumvent installation issues:*

```bash
pip install -r requirements.txt --user
```

*If this still doesn't work, you may have to append `sudo` before `pip`:*

```bash
sudo pip install -r requirements.txt --user
```

*This may require you to run in `sudo` for subsequent steps.*

*It may take a while to install the dependencies; you may want to run `pip` verbose to make sure that it's still downloading: `pip install -rv requirements.txt`*

*If you run into an error opening a port, try changing LICA's permissions: `sudo chmod 777 /dev/ttyACM0`. Alternatively, rerun everything with admin privileges.*

*If you're using OSX and getting strange errors, try:*

```bash
sudo chown -R $USER /Library/Python/3.5
```

*Installation will take longer on a Raspberry Pi, and you may need additional dependencies:*

```bash
sudo apt-get install xvfb
```

### Building LICA

To build your own LICA, check out the [Build Guide](https://github.com/maderdordor/LICA/wiki). The rest of this document will teach you how to set up the software to run the robot.

> **Note**
> You need to have the basic software set up as listed above to build LICA

### Running LICA

#### CLI

To start the CLI, plug LICA in and run

```bash
python start.py
```

_Error: could not open port. You may need to run `sudo chmod 777 <the name of the port>.`_

Ex: `sudo chmod 777 /dev/ttyACM0`

Additional flags:

- `-b` do not start up Web UI
- `-p` denote the port
- `-i` specify an IP address (won't work with localhost)

*Linux may default to a loopback IP (`127.0.1.1`); in this case you **must** specify the IP address using `-i`.*

For example, to make LICA nod with the `yes` sequence, type:

`s` -> Enter -> `yes`

Available commands:

- `l`: list available sequences
- `s`: perform a sequence, followed by the Enter key and the sequence name
- To perform an idler (looped gesture), enter two sequence names separated by `=`, e.g. `s` -> Enter -> `yes=no` (play `yes` then loop `no` indefinitely until another sequence is played).
- `q`: quit

### Interfaces

The startup prompt will say

```
+-------------------+
|     IP ADDRESS    |
+-------------------+
| 10.132.3.171:8000 |
+-------------------+
```

The IP address in this case is `10.132.3.171`. **Your IP address will be different from 10.132.3.171**

#### GUI

The GUI *should* be accessible via `localhost:8000` or `*IP address:8000` after starting up the CLI if `-b` was **not** specified. Otherwise, the CLI should print a message stating the server url.

#### Mobile App

**Installation**

Detailed instructions are available in [LICAApp](LicaApp/)

**Controlling the robot**

This allows you to control the robot's orientation (pitch, yaw, roll) by moving the phone and use sliders for the height.

Enter the IP address into the `Host` field and toggle `Control robot`. By default, the robot will copy the phone's orientation identically, i.e. the robot should be facing *away* from you. To control the robot as it's facing you, toggle `Mirror` to be `On` and the robot will gaze at the top end of the phone (like a cat looking at a laser pointer, emitting from the top of the phone).

#### Build reactions to videos

Open a new terminal and the video editor by typing: `xdg-open lica_blockly/index.html` (Ubuntu) or `open lica_blockly/index.html` (Mac), then hit "Enter." The video editor should open in a new browser or tab.

Type in the IP address into the editor and press `Update IP Address`.

To update the video, paste the URL into the field and click `Update Video`.
*Some videos have restrictions and cannot play.*

**Choreograph**

In the left side of the video editor screen, use a Gesture block and input the starting time and gesture name.

Blocks must be connected to the initial block together for them to trigger gestures.

You can create new gestures with the **mobile app** and use them in the editor video with `Reload Gestures`.

Check `Loop` box to repeat the movement indefinitely until the next gesture.

Adjust the playback speed, exaggeration (amplitude) and posture (lean forwards/backwards):

-Choose and Adjustment block and add it to the gesture blocks in the "Adjustments" part
-Enter the multiplier in the "multiply by" block.
-Connect the multiplier block to the Adjustment block
-Only one adjustment can be used at a time.

---

## Documentation & Figures

### Figure 1: Gesture Design Parameter Table
![Gesture Design Parameter Table](figures/figure1_gesture_table.png)

### Figure 2: Servo Performance Analysis
![Servo Performance Analysis](figures/figure2_servo_performance.png)

### Figure 3: Gesture Recognition Training
![Gesture Recognition Training](figures/figure3_learning_curves.png)

### Figure 4: Gesture Trajectory Validation
![Gesture Trajectory Validation](figures/figure4_trajectory_fidelity.png)

---

## About

Public Repo for the Cornell LICA Robot
