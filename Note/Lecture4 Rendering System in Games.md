# Lecture4 Rendering System in Games

## 1. Introduction to Rendering

![image-20231122000331692](./Lecture4 Rendering System in Games.assets/image-20231122000331692.png)

- Is there any game without rendering? Text Game

### Rendering on Graphics Theory

<img src="./Lecture4 Rendering System in Games.assets/image-20231122000843016.png" alt="image-20231122000843016" style="zoom:67%;" />

- Foundation of game engine rendering
- Objects with one type of effect
- Focus on representation and math correctness
- No strict performance requiement
  - Realtime 30 fps
  - Interactive 10 fps
  - Offline Rendering
  - Out-of-Core Rendering (too many data)

### Challenges on Game Rendering

![image-20231122000923845](./Lecture4 Rendering System in Games.assets/image-20231122000923845.png)

- Tens of thousands of objects with dozens type of effects

![image-20231122001020499](./Lecture4 Rendering System in Games.assets/image-20231122001020499.png)

- Deal with architecture of modern
- Computer with a complex combination of CPU and GPU

![image-20231122001058071](./Lecture4 Rendering System in Games.assets/image-20231122001058071.png)

- Commit a bullet-proof framerate
  - 30 fps, 60 fps, even 120 fps(VR)
  - 1080, 4K and 8K resolution

![image-20231122001215289](./Lecture4 Rendering System in Games.assets/image-20231122001215289.png)

- Limit access to CPU bandwidth and memory footprint
- Game logic, network, animation, physics and AI systems are major consumers of CPU and main memory

### Rendering on Game Engine

A heavily optimized practical software framework to fulfill the critical rendering requirements of games on modern hardware (PC, console and mobiles)

### Outline of Rendering

![image-20231122001452987](./Lecture4 Rendering System in Games.assets/image-20231122001452987.png)

### What is not Included

![image-20231122001658975](./Lecture4 Rendering System in Games.assets/image-20231122001658975.png)

- Cartoon Rendering
- 2D Rendering Engine
- Subsurface
- Hair / Fur

## 2. Building Blocks of Rendering

### Rendering Pipeline and Data

> Check GAMES101 for more details

![image-20231122001827842](./Lecture4 Rendering System in Games.assets/image-20231122001827842.png)

### Computation

#### Projection and Rasterization

![image-20231201212131024](./Lecture4 Rendering System in Games.assets/image-20231201212131024.png)

#### Shading

- A shader sample code
  - Constant / Parameters
  - ALU algorithms
  - Texture Sampling
  - Branches

![image-20231201212257347](./Lecture4 Rendering System in Games.assets/image-20231201212257347.png)

#### Texture Sampling

![image-20231201212416801](./Lecture4 Rendering System in Games.assets/image-20231201212416801.png)

1. Use two nearest mipmap levels
   - sample 8 pixel point, do 7 interpolation
2. Perform bilinear interpolation in both mip-maps
3. Linearly interpolate between the result

## 3. GPU

The dedicated hardware to solve massive jobs

![image-20231201212541728](./Lecture4 Rendering System in Games.assets/image-20231201212541728.png)

### SIMD and SIMT

#### SIMD Single Instruction Multiple Data

![image-20231201222340621](./Lecture4 Rendering System in Games.assets/image-20231201222340621.png)

- Describes computers with multiple processing elements that perform the same operation on multiple data points simultaneously

#### SIMT Single Instruction Multiple Threads

![image-20231201222405048](./Lecture4 Rendering System in Games.assets/image-20231201222405048.png)

- An execution model used in parallel computing where single instruction, multiple data is combined with multithreading

### GPU Architecture

![image-20231201222651048](./Lecture4 Rendering System in Games.assets/image-20231201222651048.png)

- GPC Graphics Processing Cluster
  - A dedicated hardware block for computing, rasterization, shading and texturing
- **SM Streaming Multiprocessor**
  - Part of the GPU that runs CUDA kernels
- **Texture Units**
  - A texture processing unit, that can fetch and filter a texture
- **CUDA Core**
  - Parallel processor that allow data to be worked on simultaneously by different processors
- **Wrap**
  - A collection of threads

### Data Flow from CPU to GPU

![image-20231201222906738](./Lecture4 Rendering System in Games.assets/image-20231201222906738.png)

Game Engine try to transfer data from CPU to GPU, instead of reading data from GPU

- **CPU and Main Memory**
  - Data Load / Unload
  - Data Preparation
- **CPU to GPU**
  - High Latency
  - Limited Bandwidth
- **GPU and Video Memory**
  - High Performance Parallel Rendering

### Cache Efficiency

![image-20231201223155042](./Lecture4 Rendering System in Games.assets/image-20231201223155042.png)

![image-20231201223204737](./Lecture4 Rendering System in Games.assets/image-20231201223204737.png)

- Take full advantage of hardware parallel computing
- Try to avoid the von Neumann bottleneck

### GPU Bounds and Pefroamance

- Application performance is limited by
  - Memory Bounds
  - ALU Bounds
  - TMU (Texture Mapping Unit) Bound
  - BW (Bandwidth) Bound

### Modern Hardware Pipeline

![image-20231201223414835](./Lecture4 Rendering System in Games.assets/image-20231201223414835.png)

### Other State-of-Art Architectures

#### Console

![image-20231201223520674](./Lecture4 Rendering System in Games.assets/image-20231201223520674.png)

#### Mobile Phone

![image-20231201223543520](./Lecture4 Rendering System in Games.assets/image-20231201223543520.png)

## 4. Renderable

### Mesh Render Component

<img src="./Lecture4 Rendering System in Games.assets/image-20231201223735587.png" alt="image-20231201223735587" style="zoom:67%;" />

<img src="./Lecture4 Rendering System in Games.assets/image-20231201223850733.png" alt="image-20231201223850733" style="zoom:67%;" />

- Everything is a game object in the game world
- Game object could be described in the **component-based** way
- Some component (mesh, skin) is renderable (which will be rendered on the screen)

### Mesh

<img src="./Lecture4 Rendering System in Games.assets/image-20231201223940033.png" alt="image-20231201223940033" style="zoom:67%;" />

#### Vertex and Index Buffer

<img src="./Lecture4 Rendering System in Games.assets/image-20231201224146925.png" alt="image-20231201224146925" style="zoom: 80%;" />

- Vertex Data
  - Vertex declaration
    - position
    - color
    - normal
  - Vertex buffer
- Index Data
  - Index declaration
    - index of a specific vertex
  - Index buffer

We need per-vertex normal

<img src="./Lecture4 Rendering System in Games.assets/image-20231201224505372.png" alt="image-20231201224505372" style="zoom:67%;" />



### Material

![image-20231201224539514](./Lecture4 Rendering System in Games.assets/image-20231201224539514.png)

- Determine the appearance of objects, and how objects interact with light

#### Famous Material Models

![image-20231201224655945](./Lecture4 Rendering System in Games.assets/image-20231201224655945.png)

#### Various Textures in Materials

<img src="./Lecture4 Rendering System in Games.assets/image-20231201224730788.png" alt="image-20231201224730788" style="zoom:80%;" />

### Shaders

![image-20231201224806856](./Lecture4 Rendering System in Games.assets/image-20231201224806856.png)

- A pair of code telling GPU how to execute in each vertex

### Render Objects in Engine

#### Coordinate System and Transformation

![image-20231201225022420](./Lecture4 Rendering System in Games.assets/image-20231201225022420.png)

- Model assets are made based on local coordinate systems, and eventually we need to render them into screen space

#### Object with Many Materials

![image-20231201225144201](./Lecture4 Rendering System in Games.assets/image-20231201225144201.png)

- Submit vertex & index buffer, materials parameters, textures, shader

### How to Display Different Texture on a Single Model

If every part use the same materials, it's not appear to be realistic

#### Submesh

![image-20231201225424676](./Lecture4 Rendering System in Games.assets/image-20231201225424676.png)

- split the large mesh into different submesh, each submesh uses different texture and shader

#### Resource Pool

![image-20231201225559879](./Lecture4 Rendering System in Games.assets/image-20231201225559879.png)

![image-20231201225640121](./Lecture4 Rendering System in Games.assets/image-20231201225640121.png)

- use handle to reuse resources

#### Sort by Material

![image-20231201225948905](./Lecture4 Rendering System in Games.assets/image-20231201225948905.png)

- Group different game object with the same material into one specific large mesh and pass it to GPU

#### GPU Batch Rendering

![image-20231201230155191](./Lecture4 Rendering System in Games.assets/image-20231201230155191.png)

- Group rendering all instances with identical submeshes and materials together
  - Tree, grass, etc

## 5. Visibility Culling

For each view, there are a lot of objects which aren't needed to be rendered

<img src="./Lecture4 Rendering System in Games.assets/image-20231201230327087.png" alt="image-20231201230327087" style="zoom:80%;" />

### Culling One Object

<img src="./Lecture4 Rendering System in Games.assets/image-20231201230349561.png" alt="image-20231201230349561" style="zoom:67%;" />

#### Using the simplest Bound to Create Culling

![image-20231201230421570](./Lecture4 Rendering System in Games.assets/image-20231201230421570.png)

- Inexpensive intersection texts
- Tight fitting
- Inexpensive to compute
- Easy to rotate and transform
- Use little memory

### Hierarchical View Frustum Culling

#### QTC and BVH

![image-20231201230629431](./Lecture4 Rendering System in Games.assets/image-20231201230629431.png)

![image-20231201230744185](./Lecture4 Rendering System in Games.assets/image-20231201230744185.png)

- Construction and Insertion of BVH in Game Engine
  - Adapted for dynamic moving object, easy for calculation

#### PVS

![image-20231201230835323](./Lecture4 Rendering System in Games.assets/image-20231201230835323.png)

- Divide each room into node, each corridor into edge

![image-20231201231004423](./Lecture4 Rendering System in Games.assets/image-20231201231004423.png)

- PVS Potential Visibility Set
- The idea of using PVS can be treated in different zoom in games

### GPU Culling

![image-20231201231320405](./Lecture4 Rendering System in Games.assets/image-20231201231320405.png)

## 6. Texture Compression

![image-20231201231748449](./Lecture4 Rendering System in Games.assets/image-20231201231748449.png)

- Traditional image compression like JPG and PNG
  - Good compression rates
  - Image quality
  - Designed to compress and decompress
  - an entire image
- In game texture compression
  - Decoding speed
  - Random access
  - Compression rate and visual quality
  - Encoding speed

### Block Compression

![image-20231201231841947](./Lecture4 Rendering System in Games.assets/image-20231201231841947.png)

- A 4x4 color block
- find the brightest and the darkest color
- perform interpolation between these two colors, store the distance relationship

#### Common block-based compression format

- PC: BC7, DXTC
- Mobile: ASTC, ETC/PVRTC

## 7. Authoring Tools of Modeling

### Modeling

#### Polymodeling

![image-20231201232123818](./Lecture4 Rendering System in Games.assets/image-20231201232123818.png)

#### Sculpting

![image-20231201232158005](./Lecture4 Rendering System in Games.assets/image-20231201232158005.png)

#### Scanning

![image-20231201232224091](./Lecture4 Rendering System in Games.assets/image-20231201232224091.png)

#### Procedural Modeling

![image-20231201232320875](./Lecture4 Rendering System in Games.assets/image-20231201232320875.png)

### Comparison of Authoring Methods

![image-20231201232344628](./Lecture4 Rendering System in Games.assets/image-20231201232344628.png)

## 8. Cluster-Based Mesh Pipeline

### Sculpting Tools Create Infinite Details

<img src="./Lecture4 Rendering System in Games.assets/image-20231201232544984.png" alt="image-20231201232544984" style="zoom:67%;" />

![image-20231201232502822](./Lecture4 Rendering System in Games.assets/image-20231201232502822.png)

- Artists create models with infinite details
- From linear fps to open world fps complex scene submit 10 more times triangles to GPU per-frame

### New Clusted-Based Pipeline

![image-20231201232915913](./Lecture4 Rendering System in Games.assets/image-20231201232915913.png)

![image-20231201232926072](./Lecture4 Rendering System in Games.assets/image-20231201232926072.png)

- Modern GPU can generate different details based on a block of mesh cluster

![image-20231201233112870](./Lecture4 Rendering System in Games.assets/image-20231201233112870.png)

### Nanite

![image-20231201233301010](./Lecture4 Rendering System in Games.assets/image-20231201233301010.png)

- Hierarchical LOD clusters with seamless boundary
- Don't need hardware support, but using a hierarchical cluster culling on the precomputed BVH tree by persistent threads (CS) on GPU instead of task shader

## 9. Take Away

- The design of game engine is **deeply related to the hardware** architecture design
- A **submesh** design is used to support a model with multiple materials
- Use **culling algorithms** to **draw as few objects as possible**
- As GPU become more powerful, more and more work are **moved into GPU**, which called **GPU Driven**