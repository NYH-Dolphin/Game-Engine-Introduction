# Lecture3 How to Build a Game World

## 1. Game World Objects

### Dynamic Game Objects

![image-20231121232219840](./Lecture3 How to Build a Game World.assets/image-20231121232219840.png)

- Interactable

### Static Game Objects

![image-20231121232236098](./Lecture3 How to Build a Game World.assets/image-20231121232236098.png)

- Non-Interactable

### Environments

![image-20231121232257302](./Lecture3 How to Build a Game World.assets/image-20231121232257302.png)

### Other Game Objects

![image-20231121232408973](./Lecture3 How to Build a Game World.assets/image-20231121232408973.png)

### Everything is a Game Object

- Game Object (GO)

![image-20231121232453101](./Lecture3 How to Build a Game World.assets/image-20231121232453101.png)

## 2. How to Describe a Game Object

> Want to build a drone

<img src="./Lecture3 How to Build a Game World.assets/image-20231121232532082.png" alt="image-20231121232532082" style="zoom: 33%;" />

### Properties and Behavior

- Property: Shape, Position, Capacity of battery, etc.
- Behavior: Movement

![image-20231121232644871](./Lecture3 How to Build a Game World.assets/image-20231121232644871.png)

### Inheritance / OOP

Drone vs. Armed Drone

![image-20231121232735307](./Lecture3 How to Build a Game World.assets/image-20231121232735307.png)

#### Code Example

![image-20231121232814459](./Lecture3 How to Build a Game World.assets/image-20231121232814459.png)

#### Cons

No perfect classification in the game world

![image-20231121232852645](./Lecture3 How to Build a Game World.assets/image-20231121232852645.png)

### Component Based

- Component Composition in the real world

![image-20231121233015616](./Lecture3 How to Build a Game World.assets/image-20231121233015616.png)

![image-20231121233036461](./Lecture3 How to Build a Game World.assets/image-20231121233036461.png)

![image-20231121233052127](./Lecture3 How to Build a Game World.assets/image-20231121233052127.png)

![image-20231121233153092](./Lecture3 How to Build a Game World.assets/image-20231121233153092.png)

#### Code Example

![image-20231121233138501](./Lecture3 How to Build a Game World.assets/image-20231121233138501.png)

#### Components in Commercial Engines

![image-20231121233225390](./Lecture3 How to Build a Game World.assets/image-20231121233225390.png)

## 3. How to Make the World Alive

### Object-based Tick

![image-20231121233542085](./Lecture3 How to Build a Game World.assets/image-20231121233542085.png)

- Simple and Intuitive
- Easy to debug

### Component-based Tick

![image-20231121233652998](./Lecture3 How to Build a Game World.assets/image-20231121233652998.png)

- Parallelized processing
- Reduced cache miss
- More efficient

![image-20231121233928219](./Lecture3 How to Build a Game World.assets/image-20231121233928219.png)

## 4. How to Interact between Game Objects

### Hardcode

![image-20231121234110878](./Lecture3 How to Build a Game World.assets/image-20231121234110878.png)

### Events

![image-20231121234202249](./Lecture3 How to Build a Game World.assets/image-20231121234202249.png)

- Message sending and handling
- Decoupling event sending and handling
- Encapsule the message into an event
- Decoupling 

#### Event Mechanism in Commercial Engines

![image-20231121234313841](./Lecture3 How to Build a Game World.assets/image-20231121234313841.png)

## 5. How to Manage Game Objects

> The bomb effects all the game objects in the scene

### Scene Management

![image-20231121234539197](./Lecture3 How to Build a Game World.assets/image-20231121234539197.png)

- Game objects are managed in a scene
- Game object query
  - By **unique game object ID**
  - By object position

#### No division

![image-20231121234632841](./Lecture3 How to Build a Game World.assets/image-20231121234632841.png)

- Notify all the game objects in the scene
- $O(n^2)$ challenge

#### Divided by grid

![image-20231121234735470](./Lecture3 How to Build a Game World.assets/image-20231121234735470.png)

- Find the neighbor grid
- Cons: game objects in the scene are not equally distributed

#### Hierarchical Segmentation

![image-20231121234902248](./Lecture3 How to Build a Game World.assets/image-20231121234902248.png)

- Segmented space by object clusters

  ![image-20231121234917635](./Lecture3 How to Build a Game World.assets/image-20231121234917635.png)

![image-20231121235032046](./Lecture3 How to Build a Game World.assets/image-20231121235032046.png)

### Spatial Data Structures

![image-20231121235111387](./Lecture3 How to Build a Game World.assets/image-20231121235111387.png)

- Is the core in game engine and scene management
- Implement in different structure due to different game

## 6. Other

### GO Bindings

![image-20231121235446869](./Lecture3 How to Build a Game World.assets/image-20231121235446869.png)

- When player is bound with a tank, how to tick
- Tick father game objects the first, and then tick the child game objects

### Component Dependencies

![image-20231121235803019](./Lecture3 How to Build a Game World.assets/image-20231121235803019.png)

- The sequence to tick the component is important (May in parallel execution)
- Different components can send message to each other simultaneously
- We want the game to be deterministic

### Post Office

![image-20231121235754929](./Lecture3 How to Build a Game World.assets/image-20231121235754929.png)

- Post office takes charge of all the messages
- Pre-tick and Post-tick to solve the sequential problem

## 7. Summary

- Everything is a game object in the game world
- Game object could be described in the component-based way
- States of game objects are updated in tick loops
- Game objects interact with each other via event mechanism
- Game objects are managed in a scene with efficient strategies
