---
layout: default
title: "Before the AI Era: Field-Tested Foundations"
permalink: /projects/field-tested-foundations/
---

# Before the AI Era: Field-Tested Foundations

Field-tested foundations of how I build: seeing a real problem, building the missing system, and iterating until it works.

## Overview

A lot of my engineering work starts the same way: I see a real-world bottleneck, sketch the system that could remove it, build the missing pieces, and keep fixing the messy parts until the system works.

This page collects earlier systems work that shaped that habit: robotics and embedded prototypes, automated Wi-Fi CSI measurement, drone-based aerial connectivity experiments, and motorized antenna systems. The common thread is not a single technology stack. It is the decision to build something physical or operational when the problem could not be answered cleanly from a desk.

## Early Robotics and Physical Prototyping

Early hands-on projects taught me how messy real systems can be. I worked with RFID-based object tracking ideas, CNC machining, 3D printing, motor control, embedded boards, wireless-controlled robots, waterproofing, batteries, modular robot structures, and power-line communication under limited time, budget, and manpower.

One early idea was a smart bag that could recognize which RFID-tagged books were inside and compare them with a daily timetable. It was more important as an idea than as a polished product: it taught me to look at an ordinary annoyance and ask what kind of physical sensing system could remove it.

Other projects were more mechanical. I built a large ball-shaped mobile robot that changed direction by moving its center of mass inside the shell, supported wireless control, and was designed as a modular base that could pull or carry additional functions. I also worked on an underwater exploration robot, where the lessons were different: waterproofing, batteries, module boundaries, and power-line communication became part of the engineering problem.

The important lesson was not any single tool. It was the habit of making ideas physical, then fixing the mechanical, electrical, software, and environmental problems that appeared only after the system started to exist.

## Automated Wi-Fi CSI Measurement Rig

I needed to measure Wi-Fi CSI at many precise antenna positions, but the experiment was too repetitive and position-sensitive to run by hand. A person can move an antenna for a while; a person should not be the positioning system for a massive measurement campaign.

The key idea was to treat a large laser engraver not as a laser tool, but as a precise two-axis motion platform. I proposed using the motion system without the laser, then combined serial coordinate control with Python automation so the setup could move the antenna and collect channel measurements continuously.

This turned a tedious manual experiment into a repeatable measurement rig. It could place the antenna at controlled positions, run long measurement sequences, and collect Wi-Fi channel data for experiments where spatial accuracy and repetition mattered. Some campaigns could run for many hours, or even longer, without asking a human to keep doing the same motion by hand.

This setup later supported Wi-Fi CSI research where accurate and repeatable spatial measurement mattered.

## Drone-based Aerial Connectivity Measurement Platform

Aerial connectivity is hard to understand only from ground assumptions. A phone in the air sees the network from a different height, geometry, and radio environment. To measure that directly, I mounted smartphones on drones and built custom Android measurement tools to log throughput, signal quality, serving-cell information, and flight-related context during aerial experiments.

The engineering problem was larger than putting a phone on a drone. The drone had to carry the smartphone payload reliably, the mounting had to be stable but removable, and the data had to be accessible after each flight. The measurement app also had to reduce field-work friction: one practical feature used altitude changes to detect takeoff and landing, then segment and save measurement logs around each mission.

I also had to understand what the phone was connected to, not only whether it had signal. That meant investigating serving-cell information, measurement APIs, available public cell-site information, and the limits of what a normal mobile device could report in the field.

The result was a practical aerial measurement platform: drone, smartphone, Android logging app, flight mission, raw measurement logs, and offline analysis pipeline. The platform later supported research on aerial cellular connectivity.

## Motorized Antenna Polarization Measurement System

For polarization-related wireless experiments, I needed more than a model. I needed a way to rotate a real antenna in the air, control it remotely, and compare the measurement with MATLAB-based analysis.

I built a drone-mounted motorized antenna setup using a Raspberry Pi with cellular connectivity, remote Linux access, Python-based GPIO control, and two servo motors arranged in series to rotate the antenna across controlled angles. The system connected mathematical modeling, simulation, antenna orientation, motor control, remote access, drone payload constraints, and RF measurement into one experiment.

The hardest parts were not only the equations. The experiment became a full system integration problem: RF behavior, mechanical mounting, motor control, remote access, drone payload, field safety, signal isolation, and data reliability all had to work together.

One of the most memorable debugging moments came when the system still communicated even after the antenna was disconnected. The signal was leaking through the device itself. To make the measurement trustworthy, I wrapped the non-antenna parts with physical shielding using foil and copper tape until the connection depended on the antenna path as intended.

It was a small, physical fix, but it captured the kind of engineering I enjoy: finding the real reason an experiment is lying, then changing the system until the measurement becomes trustworthy.

## What Carried Forward

These projects are why I do not think of connectivity as only “making devices connect.” Wireless signals can become measurement tools, localization clues, sensing inputs, and data sources for learning-based systems.

They also shaped how I work today. I am drawn to problems where the useful answer is not only a model or a slide, but a system: a tool, a measurement workflow, a prototype, an automation loop, or a device setup that survives contact with the real world.

That perspective still informs how I think about mobile connectivity, Bluetooth/Wi-Fi sensing and ranging, localization, and AI-assisted engineering workflows.
