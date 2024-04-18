# MEC1003F Lecture 3 Demo

KiCad Demonstration Project for UCT MEC1003F 2024.

## Lesson Plan

In this lecture we will continue from the previous project's schematic. In the last lecture we made some footprints and assigned them to the schematic components. In the assignment we also added a voltage regulator to the same circuit. Either project can continue to be used for this lecture, but this project will be used as the reference.

The lecture will also contain a fair bit of information on the PCB manufacturing process, which is not detailed in this project.

## Overview

This project retains the original project structure as previously used. The main project [MEC1003F 2024 Lecture 3 Demo.kicad_pro](MEC1003F%202024%20Lecture%203%20Demo.kicad_pro) contains:

- A single Schematic file [MEC1003F 2024 Lecture 3 Demo.kicad_sch](MEC1003F%202024%20Lecture%203%20Demo.kicad_sch).
- A single PCB file [MEC1003F 2024 Lecture 3 Demo.kicad_pcb](MEC1003F%202024%20Lecture%203%20Demo.kicad_pcb).
- A project symbols library [Project Symbols.kicad_sym](Project%20Symbols.kicad_sym).
- A project footprints library [Project Footprints.pretty](Project%20Footprints.pretty).

Today we are going to focus on the PCB file.

## PCB Information

Before we start laying out routing the PCB, we must learn a bit about how PCBs are made in order to understand the limitations our design must adhere to. The first bif of the lecture will cover this.

## PCB Layout & Routing

Now that we are familiar with the PCB manufacturing process, we can start doing something! Today we will over the following tasks:

### Task 1: Design Rules

Before we start routing, we need to set up the design rules. This is done in the `Design Rules` section under the `File > Board Setup` menu. The design rules are the constraints that the PCB layout must adhere to in order to be manufacturable. The design rules are set by the manufacturer and are usually available on their website. We must translate these rules into KiCad's design rules.

For this lecture we will follow the design rules of [JLCPCB](https://jlcpcb.com/). The design rules are available at [https://jlcpcb.com/capabilities/Capabilities](https://jlcpcb.com/capabilities/Capabilities).

In the lecture I will walk the class through this. It is not a 1:1 translation! The manufacturer capabilities are the absolute limit, and it is good engineering practice to give some margin on these specs. For example, the minimum trace width is 0.127mm, but we will use 0.30mm. You must use your judgement based on the design requirements, the manufacturer's capabilities, and the sensitivity of these specifications when setting the design rules.

### Task 2: Board Outline

The board outline is the physical boundary of the PCB. In KiCad the board outline is set in the `Edge.Cuts` layer with a simple closed path using the drawing tools. For this demo there is no requirements for a complex shape, and for the amount of components we have, a simple 30x30mm square will suffice.

Place a board outline by using the rectangle drawing tool in the `Edge.Cuts` layer.

### Task 3: Component Placement

In the demo project I did some component placement already for half the circuit. It is hard to really teach component placement, it's very much subjective and there's a degree of style to it, especially when there are no electromagnetic or thermal requirements. But there are some general guidelines:

- Set as high a grid scale as possible for the components you are placing. This makes it easier to align and stop worrying about exact locations.
- Hide the silkscreen and other unnecessary layers. Those are secondary concerns to be dealt with later.
- Place the things which must be at a particular location first. This mostly means connectors and mechanical mounting holes. Easy enough. As for the rest...
- Orient passive components around the central component (usually some integrated circuit) that they are supporting. This brings a logical grouping to the components, like how the schematic would have been drawn. Do this to the side in free space - do not consider the rest of the board yet. Just focus on this group of components fitting well with each other. Repeat for each group of components.
- Place passive components in rows along the face of the IC. It looks right and simplifies things. Don't try overcomplicating the layout - there is likely to be zero functional benefit.
- Don't route the components yet. Just place them, or only route obvious and short connections. It becomes harder to move components once they are routed. The rats nest lines will rather show you if the routing will be simple with the layout until you're ready to go.
- Use vias sparingly, but use them. They don't add any cost, the main impact is the space they take up. At a certain point that space is worth it though over long meandering traces.
- All power and ground nets, just route to a quick via. Drop it to the bottom later and move on. GND will connect to a ground plane and power we'll deal with later.
- A good rule of thumb is to set a trace with that us 60-80% of the pad width you're starting from. It looks good, and if the trace needed to be thicker then probably the pad would be bigger too. Only increase the trace width along the track length if you have a reason, like if it is a long trace.
- Polygons can be used for power planes, but while we only have a 2 layer board without any high power components we can simply route power like any other trace. You can use power plane polygons when you have more layers and more complex power delivery requirements.
- Once a subcircuit is laid out and routed, move that group can be considered a unit and placed on the board space accordingly. With a bigger shape it will be more obvious to see which orientation and location is best.

It is a long process and the only way to do it quickly is with some practise. For this assignment, simply layout, route, delete and repeat until you are happy with your speed and the result.

### Task 4: Gerber Files

The final task in this lecture is to generate the Gerber files. These are the files that the PCB manufacturer will use to make the PCB.

## Next Lecture

That is the end of this course's core content! You should now know how to make a simple PCB from start to finish. The next lecture is dedicated to preparation for the class test, where I will demonstrate what you will be asked to do under test conditions.

I'll do this test demo in less than the allocated time, so I'll also show you some of the things I skipped over earlier, like the Electric Rules Checker and multipart symbols, which are good to know but not essential for the test. I'll also show what is needed for automatic assembly for JLCPCB, which requires some extra information to be added to the Bill of Materials and Pick n Place files.
