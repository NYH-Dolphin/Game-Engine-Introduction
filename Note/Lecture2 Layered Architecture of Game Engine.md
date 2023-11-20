# Lecture2 Layered Architecture of Game Engine

## 1. Sea of Codes - Where to begin

### A Glance of Game Engine Layers

![image-20231120113010622](./Lecture2 Layered Architecture of Game Engine.assets/image-20231120113010622.png)

#### Tool Layer - Chain of Editors

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120112322301.png" alt="image-20231120112322301" />

#### Function Layer - Make it visible, movable and playable

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120112404235.png" alt="image-20231120112404235" />

#### Resource Layer - Data and Files

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120112457059.png" alt="image-20231120112457059" />

#### Core Layer - Swiss Knife of Game Engine

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120112651137.png" alt="image-20231120112651137" />

#### Platform Layer - Launch on Different Platforms

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120112757457.png" alt="image-20231120112757457" />

#### Middleware and Third party Libraries

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120112925225.png" alt="image-20231120112925225" />

### Why Layered Architecture

![image-20231120142746793](./Lecture2 Layered Architecture of Game Engine.assets/image-20231120142746793.png)

- Decoupling and Reducing Complexity
  - Lower layers are independent from upper layers
  - Upper layers don't know how lower layers are implemented
  - Upper layer can call lower layer, but lower layer can not call upper layer
- Response for Evolving Demands
  - Upper layers **evolve fast**, but lowers are **stable**

## 2. Practice is the Best Way to Learn

### Task - Simple Animated Character Challenge

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120113144669.png" alt="image-20231120113144669" />

- Create, animate and render a character
- Playable on selected hardware platform

### Resource - How to Access my Data

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120134659003.png" alt="image-20231120134659003" style="zoom:80%;" />

Offline Resource Importing

- Unify file access by defining a **meta asset** file format (eg, `.ast`)
  - easier for GPU to use
  - assets are faster to access by importing preprocess
- Build a **composite asset** file to refer to all resources
- **GUID** is an extra protection of reference
  - asset identity

#### Runtime Asset Manager

![image-20231120135336681](./Lecture2 Layered Architecture of Game Engine.assets/image-20231120135336681.png)

- A virtual file system to load/unload assets by path reference
- Manage asset lifespan and reference by handle system

#### Manage Life Cycle

![image-20231120135505510](./Lecture2 Layered Architecture of Game Engine.assets/image-20231120135505510.png)

- Different resources have different life cycles
- Limited memory requires release of loaded resources when possible 
- Garbage collection and deferred loading is critical features

### Function - How to Make the World Alive

#### Dive into Ticks

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120135728048.png" alt="image-20231120135728048" style="zoom:80%;" />

- tick: experience all the functions with 1/30s to make the game looks natural

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120135845329.png" alt="image-20231120135845329" />

- `tickLogic` and `tickRender` are two different aspects

#### Tick the Animation and Renderer

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120140311806.png" alt="image-20231120140311806" />

- In each tick (over-simplified version)
  - Fetch animation frame of character
  - Drive the skeleton and skin of character
  - Renderer process all rendering jobs in an iteration of render tick for each frame

#### Function is Heavy-duty Hotchpotch

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120140520029.png" alt="image-20231120140520029" />

- Function Layer provides major function modules for the game engine 
  - Object system (HUGE)
- Game Loop updates the systems periodically
  - Game Loop is the key of reading codes of game engines
- Blur the boundary between engine and game 
  - Camera, character and behavior
  - Design extendable engine API for programmer

#### Multi-Threading

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120140622248.png" alt="image-20231120140622248" />

- **Multi-core processors** become the mainstream
  - Many systems in game engine are built for parallelism

### Core - Foundation of Game Engine

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120141800593.png" alt="image-20231120141800593" />

- Core layers provide utilities needed in various function modules 
- Super high performance design and implementation 
- High standard of coding

#### Math Library

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120140825957.png" alt="image-20231120140825957" />

- Linear algebra
  - Rotation, translation, scaling
  - Matrix splines, quaternion

#### Math Efficiency

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120140919262.png" alt="image-20231120140919262" style="zoom:80%;" />

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120141010243.png" alt="image-20231120141010243" />

#### Data Structure and Containers

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120141126246.png" alt="image-20231120141126246" />

- Vectors, maps, trees, etc.
- Customized outperforms STL
- Avoid fragment memory

#### Memory Management

- Major bottlenecks of game engine performance
  - Memory Pool / Allocator
  - Reduce cache miss
  - Memory alignment
- Polymorphic Memory Resource (PMR)

For game engine, it will request a large amount of memory at once, and then arrange on that basis

How to make memory management fast

- Put data together
- Access Data in Order
- Allocate and De-allocate as a block

### Platform - Target on Different Platform

#### File system

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120141926001.png" alt="image-20231120141926001" />

Compatibility of different platforms, provides platform-independent services and information for upper layers

- Path: Slash/Backslash, Environment variables
- Directory Traversal

#### Graphics API

**Render Hardware Interface (RHI)**

- Transparent different GPU architecture and SDK
- Automatic optimization of target platforms

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120142018197.png" alt="image-20231120142018197" />

#### Hardware Architecture

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120142207200.png" alt="image-20231120142207200" />

### Tool - Allow Anyone to Create Game

<img src="./Lecture2 Layered Architecture of Game Engine.assets/image-20231120142340614.png" alt="image-20231120142340614" />

- Unleash the creativity
  - Build upon game engine
  - Create, edit and exchange gameplay assets
- Flexible of coding languages
  - C++, C#, HTML

### Digital Content Creation (DCC)

![image-20231120142614653](./Lecture2 Layered Architecture of Game Engine.assets/image-20231120142614653.png)

## 3. Mini Engine - Pilot

> https://github.com/BoomingTech/Piccolo

![image-20231120143628081](./Lecture2 Layered Architecture of Game Engine.assets/image-20231120143628081.png)

### Introduction

- Build by C/C++
  - Runtime: ~13,000 lines
  - Editor: ~2,000 lines
- Follow Engine Layers
  - Source code still improving
- Support Platform
  - Windows
  - Linux
  - MacOS

### Function

- Basic Editing
  - Add/Delete Objects
  - Move/Scale/Rotate objects
- Simple Functions
  - Character control
  - Camera

