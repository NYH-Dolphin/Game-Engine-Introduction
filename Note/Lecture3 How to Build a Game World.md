# Lecture3 How to Build a Game World

## 1. Game World Objects

### Dynamic Game Objects

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232219840.png" alt="image-20231121232219840" />

- Interactable

### Static Game Objects

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232236098.png" alt="image-20231121232236098" />

- Non-Interactable

### Environments

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232257302.png" alt="image-20231121232257302" />

### Other Game Objects

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232408973.png" alt="image-20231121232408973" />

### Everything is a Game Object

- Game Object (GO)

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232453101.png" alt="image-20231121232453101" />

## 2. How to Describe a Game Object

> Want to build a drone

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232532082.png" alt="image-20231121232532082" style="zoom: 33%;" />

### Properties and Behavior

- Property: Shape, Position, Capacity of battery, etc.
- Behavior: Movement

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232644871.png" alt="image-20231121232644871" />

### Inheritance / OOP

Drone vs. Armed Drone

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232735307.png" alt="image-20231121232735307" />

#### Code Example

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232814459.png" alt="image-20231121232814459" />

#### Cons

No perfect classification in the game world

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232852645.png" alt="image-20231121232852645" />

### Component Based

- Component Composition in the real world

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233015616.png" alt="image-20231121233015616" />

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233036461.png" alt="image-20231121233036461" />

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233052127.png" alt="image-20231121233052127" />

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233153092.png" alt="image-20231121233153092" />

#### Code Example

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233138501.png" alt="image-20231121233138501" />

#### Components in Commercial Engines

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233225390.png" alt="image-20231121233225390" />

## 3. How to Make the World Alive

### Object-based Tick

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233542085.png" alt="image-20231121233542085" />

- Simple and Intuitive
- Easy to debug

### Component-based Tick

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233652998.png" alt="image-20231121233652998" />

- Parallelized processing
- Reduced cache miss
- More efficient

<img src="./Lecture3 How to Build a Game World.assets/image-20231121233928219.png" alt="image-20231121233928219" />

## 4. How to Interact between Game Objects

### Hardcode

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234110878.png" alt="image-20231121234110878" />

### Events

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234202249.png" alt="image-20231121234202249" />

- Message sending and handling
- Decoupling event sending and handling
- Encapsule the message into an event
- Decoupling 

#### Event Mechanism in Commercial Engines

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234313841.png" alt="image-20231121234313841" />

## 5. How to Manage Game Objects

> The bomb effects all the game objects in the scene

### Scene Management

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234539197.png" alt="image-20231121234539197" />

- Game objects are managed in a scene
- Game object query
  - By **unique game object ID**
  - By object position

#### No division

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234632841.png" alt="image-20231121234632841" />

- Notify all the game objects in the scene
- $O(n^2)$ challenge

#### Divided by grid

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234735470.png" alt="image-20231121234735470" />

- Find the neighbor grid
- Cons: game objects in the scene are not equally distributed

#### Hierarchical Segmentation

<img src="./Lecture3 How to Build a Game World.assets/image-20231121234902248.png" alt="image-20231121234902248" />

- Segmented space by object clusters

  <img src="./Lecture3 How to Build a Game World.assets/image-20231121234917635.png" alt="image-20231121234917635" />

<img src="./Lecture3 How to Build a Game World.assets/image-20231121235032046.png" alt="image-20231121235032046" />

### Spatial Data Structures

<img src="./Lecture3 How to Build a Game World.assets/image-20231121235111387.png" alt="image-20231121235111387" />

- Is the core in game engine and scene management
- Implement in different structure due to different game

## 6. Other

### GO Bindings

<img src="./Lecture3 How to Build a Game World.assets/image-20231121235446869.png" alt="image-20231121235446869" />

- When player is bound with a tank, how to tick
- Tick father game objects the first, and then tick the child game objects

### Component Dependencies

<img src="./Lecture3 How to Build a Game World.assets/image-20231121235803019.png" alt="image-20231121235803019" />

- The sequence to tick the component is important (May in parallel execution)
- Different components can send message to each other simultaneously
- We want the game to be deterministic

### Post Office

<img src="./Lecture3 How to Build a Game World.assets/image-20231121235754929.png" alt="image-20231121235754929" />

- Post office takes charge of all the messages
- Pre-tick and Post-tick to solve the sequential problem

## 7. Summary

- Everything is a game object in the game world
- Game object could be described in the component-based way
- States of game objects are updated in tick loops
- Game objects interact with each other via event mechanism
- Game objects are managed in a scene with efficient strategies
