---
layout: default
---

# Space Pilot Simulator
Space Pilot is a very short proof of concept where the player is placed inside of a futureist dropship and has to pilot the VTOL craft in 3D space.

The player can freely look around and interact with the various consoles on the craft to operate it. Interacting with the various physical and screen buttons will send instrutions to the Flight Control System which will drive the crafts thrusters to match the players intentions.

## Interactive Screens & Physicalised Controls.
The ships controls are built up of interactive screens and buttons that can be pressed with a mouseclick of the user, when the user holds down the F key (by default) they can see their mouse and easily interact with the ships controls.

Before the ship can fly a preflight startup needs to be done by the pilot, beginning with activating the power and then initating the Flight Control System startup - Once the Flight Control System has done its preflight anaylsis of the craft the user will be given control.

## The Flight Control System.
The player could not possibly drive all the control surfaces and thrusters on the craft, so instead control of the ship is abstracted away from the player like it would be in a modern aircraft by the Flight Control System.

The Flight Control System attempts to best interpret the players inputs and drives all the various systems across the craft. It sets itself velocity targets based on player inputs and makes the craft match those vectors.

The craft itself is very modular, and on startup of the craft by player input the Flight Control System will do a dynamic startup and identify all the control surfaces, thrusters and systems it has avaliable to it. It will even print the output of the bootup to all the panels in the craft to inform the player of what the status of the ship is, after the boot has finished all the panels will switch to their deault screens.

## Flight Model
The flight model allows the ship to operate in both atmosphere and space, allowing the user to comfortably control the ship in different enviorments where exterior forces acting on the ship might not be present - i.e. air resitance or gravity.

The flight model also models the control surfaces of the craft, at high speeds in an atmosphere the control surfaces have a larger affect on the craft than they would at low speeds. The control surfaces are also control by the Flight Control System and dynamically affect the crafts movement, to roll the craft airlerons activate and produce forces proportional to there distance from the centre of gravity and the air flowing over them.

### [Return to the homepage](./)
