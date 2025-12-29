# Project Overview

This project documents the design of a 15 kg combat robot (battlebot) for Robowars‑style competitions, focusing on mechatronic system design, drivetrain sizing, weapon actuation, and electrical subsystem selection. The goal was to design a robust, remotely operated, two‑wheeled drum‑spinner robot that can traverse the arena quickly, survive impacts, and reliably deliver weapon strikes within the competition budget and rules.

This project is hosted at : [https://github.com/SatvikS3638/Battlebot]

![Combat Robot Chassis](assets\images\chassis)

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
$N=\frac{V}{2\pi R}≈7.32rev/s≈220rpm$ 

This RPM served as a target for the wheel motor selection so that the bot can meet the agility requirement without over‑gearing the drivetrain.

## Acceleration Requirement
Typical combat robot guidelines suggest an acceleration magnitude on the order of half the target velocity over one second. Using this rule of thumb, a design acceleration of approximately 0.57 m/s² was adopted for sizing the drivetrain torque.

## Traction and Torque Estimates
Assuming a maximum robot weight of 15 kg and a worst‑case engagement where the effective load on the wheels can temporarily double (up to 30 kg), the load per wheel was estimated at about 7.5 kg for a four‑wheel configuration. Using this load and the 50 mm wheel radius, the static torque requirement per wheel was computed as approximately 0.375 Nm (37.5 Ncm).
To provide a robust margin, an additional rule from combat robotics practice was applied: each drive motor’s stall torque should be sufficient to lift the full robot weight at the wheel radius. Using a 15 kg robot, the required stall torque per motor becomes:
$T_{stall}=mgr=15x9.8x0.05≈7.35Nm$
This requirement drove the choice of geared drive motors with sufficiently high stall torque.

## RMF (Robot Motor Factor) Check
The drivetrain design was validated using an online Robot Motor Factor (RMF) calculator, which consolidates robot weight, wheel radius, and speed into a single metric. With the chosen parameters, the RMF requirement was around 6.9 kg·m·rev/s, and motors meeting or exceeding this RMF were considered acceptable.

# Weapon (Drum Spinner) Design

![Drum Spinner Design](assets/images/spinner) 

## Worst‑Case Load Modelling
The drum spinner motor was sized for an extreme case where the entire opponent robot’s weight rests on the drum, even though this scenario is unlikely in practice. Taking an opponent mass of up to 15 kg and assuming a friction coefficient up to 1, the maximum normal force on the drum can be approximated as:​
$F_{max}≈2xM_{2}g≈294N$
Here, a safety factor of 2 was included to account for dynamic impacts and uncertainties.
With the drum radius constrained to 50 mm, the corresponding resistive torque is:
$T_{drum}=F_{max}xr≈294x0.05≈14.7Nm$
This torque is intentionally conservative; in practice, such a load is rarely sustained, so the design decision was to select a “very high torque” motor and prioritize robustness rather than exactly meeting this extreme torque.

## Motor Selection Strategy
The primary criteria for the drum motor were:
* High torque at operating speed to spin up the drum quickly and resist stalling during impact.
* Thermal robustness so that the motor does not overheat or fail under repeated high‑torque, high‑current operation.
* Compatibility with available ESCs and supply voltage (around 11–12 V), and alignment with overall budget limits.

# Electronics and Control System
## Motor Control (ESCs and Drivers)
For brushless motors, compact drone‑type ESCs rated at 40 A and above were considered, offering good availability and cost‑effectiveness in the sub‑₹1000 range per unit. The ESC continuous current ratings were chosen to exceed the maximum motor current at stall or peak load, and physical size was considered to ensure adequate heat dissipation during matches.
For brushed motors, high‑current ESCs were harder to source locally within budget, so a microcontroller‑plus‑motor‑driver architecture was evaluated. In this configuration:
*  A microcontroller (e.g., Arduino Uno) handles RC signal decoding and PWM generation.
*  Dual and single high‑current DC motor drivers (e.g., 13 A continuous, 30 A peak modules) drive the wheel and weapon motors.

## Power System (Batteries)
LiPo batteries were selected for their high energy density and discharge capability. A typical option considered was a 3‑cell (11.1 V) LiPo pack with capacity up to 3000 mAh as a modular solution, and a single larger 8000 mAh 3S pack as an integrated high‑capacity option.
Key design considerations:
* Discharge rating (C‑rating) sufficient to supply combined peak current of drive and weapon systems over the match duration.
* Trade‑off between using multiple smaller cells for better packaging and weight distribution versus a single larger pack for simplicity.
* Overall battery cost and availability in the Indian market.

## RC Transmitter and Receiver
A 2.4 GHz RC system with at least 6 channels was selected to provide headroom for drive, weapon, and potential future auxiliaries. An affordable Flysky transmitter–receiver pair was chosen, offering sufficient functionality for combat robots while remaining accessible for student teams.
Important RC system features:
* Matching protocol between transmitter and receiver for reliable communication.
* Built‑in BEC on ESCs or dedicated BEC to power the receiver at the appropriate voltage and current.
* Support for forward, reverse, and mixed control (tank steering), plus a compliant trip/failsafe mechanism as per competition safety rules.

# Component Selection and Budget
## Final Component List (Representative)
The following components were shortlisted based on the above requirements and calculations:
* RC System: Flysky CT6B 2.4 GHz 6‑channel transmitter with receiver, providing sufficient channels for two drive motors and one weapon motor.
* Wheel Motors: Two planetary geared DC motors satisfying the 7.35 Nm stall torque requirement and RMF criterion, with per‑motor costs in the ₹2000–₹2500 range.
* Weapon Motor: A high‑torque 12 V planetary gear motor (e.g., 100 rpm, ≈294 N·cm rated torque) chosen to deliver strong drum acceleration and sustained torque.​
* Motor Drivers/Controllers:
  - Option A: Three 50 A ESCs for a brushless architecture (2 drive + 1 weapon), using drone‑grade ESCs.
  - Option B: Microcontroller (e.g., Arduino Uno) plus dual and single high‑current DC motor driver modules for a brushed architecture.
* Battery: Either a modular 3S LiPo setup around 11.1 V and 3000 mAh per pack, or a single 3S 8000 mAh pack, selected based on weight and runtime trade‑offs.

Approximate line‑item prices were compiled from local robotics and e‑commerce vendors to ensure the entire system fits within a student competition budget, with motor and battery choices having the largest cost impact.
