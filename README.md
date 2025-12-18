# Project Overview

This project documents the design of a 15 kg combat robot (battlebot) for Robowars‑style competitions, focusing on mechatronic system design, drivetrain sizing, weapon actuation, and electrical subsystem selection. The goal was to design a robust, remotely operated, two‑wheeled drum‑spinner robot that can traverse the arena quickly, survive impacts, and reliably deliver weapon strikes within the competition budget and rules.

# System Requirements
## Competition and Performance Targets
* Maximum robot weight: 15 kg (Robowars class limit).
* Locomotion: Two‑wheel differential drive with independent wheel motors.
* Weapon: Front‑mounted horizontal drum spinner capable of delivering high‑energy impacts.
* Mobility target: Traverse the arena diagonal (approximately 16 ft) in about 6 seconds, with adequate acceleration for combat maneuvers.

## Mechanical Constraints
* Maximum practical wheel diameter identified from available COTS wheels: 100 mm (10 cm).
* Wheel width options considered: approximately 20 mm and 46 mm, chosen for robustness and traction in a combat environment.
* Drum spinner radius constrained to be no larger than wheel radius (≈50 mm) to maintain ground clearance and packaging compatibility

## Electrical and Control Constraints
* Remote control via RC transmitter–receiver pair with at least 3 channels (2 drive channels + 1 weapon channel).
* Power system using LiPo chemistry for high discharge rates and low weight.
* Use of COTS ESCs or motor drivers compatible with selected brushed/brushless motors and current requirements.

# Drivetrain Design
## Velocity and RPM Calculations
To ensure adequate mobility, the required linear speed V was computed assuming the robot must cross the diagonal of the arena in about 6 seconds. For a 16 ft square arena, this yields a required velocity of approximately 1.15 m/s. 
For a wheel radius R ≈ 0.05 m (10 cm diameter), the required wheel rotational speed N is: 
$ N = \frac{V}{2\pi R} ≈ 7.32 rev/s ≈ 220 rpm $ 
