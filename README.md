# ftcsim
# FTC Programming Practice

Code written while teaching myself Java and FTC-specific programming — coming from a Python background — over a few weeks of self-directed practice in FTCSIM, ahead of applying for my school's FTC programming team.

## EncoderAutonomous.java
Moves the robot a set distance and executes a turn using encoder tick counts instead of timed (`sleep()`) driving. Timed driving was inconsistent between runs (battery voltage, floor friction), so this uses `RUN_TO_POSITION` mode and waits on `isBusy()` to know when the robot has actually arrived — repeatable regardless of those variables.

## ColourDetectionAutonomous.java
Detects a colour panel using distance and colour sensors, then reacts to it. Includes a fix for a real bug I hit: the robot kept re-triggering the same manoeuvre repeatedly (rapid spinning) because the colour condition was still true on the very next loop check. Fixed using boolean flags so each manoeuvre only fires once, and a proper loop (rather than a single snapshot check) that waits until the robot has genuinely moved clear before considering itself done.

## DecodeAutonomous.java
A simplified version of the actual AUTO period logic in this season's game (DECODE, 2025–26): drive to a scoring area, read a sensor to classify what's there, branch based on that, then return to base. Built from the same encoder and sensor patterns as the other files, adapted to reflect this season's game structure (detect → classify → act → return) after reading the official game manual.

## FreightFrenzyAutonomous.java
A simplified look at the 2021–22 season's game (Freight Frenzy): reads a sensor value standing in for the randomised "barcode" read at the start of AUTO, then drives to one of three positions representing the shipping hub's three scoring levels.

## PowerPlayAutonomous.java
A simplified look at the 2022–23 season's game (Power Play): drives to a "junction" using distance sensing rather than guessed timing, then picks a parking zone based on a sensor reading standing in for the randomised signal cone used in the real game's endgame.

## Notes
None of these are built against real field elements or hardware — they're written and tested in FTCSIM, focused on demonstrating the core control patterns (closed-loop distance/heading control, sensor-triggered branching, avoiding common bugs like re-triggering loops) rather than full game mechanics.
