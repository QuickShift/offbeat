# offbeat

Offbeat - Particle Effects System

A project mainly inspired by the Destiny particle system, reviewed and explained in detail in the SIGGRAPH 2017 Advances in Real-Time Rendering in Games course. That was not the only source of information though. List of all the resources/references can be found at the end of this README.

This project was also an attempt at creating a decent API for convenient usage in other custom game engines. However, at least currently, the API is far from decent and, in my opinion, is only "usable".

The Offbeat particle effects system was presented as my bachelor's degree final project.

### Game engine

The system was developed in the [ngpe engine](https://github.com/2-tuple/Engine) -- a custom game engine that my friend and I worked on. Thus, the proper commit history can be seen in the [particle_system](https://github.com/2-tuple/Engine/tree/particle_system) branch of the project. This repository, however, contains only the code of the particle system, meaning the code in this repository cannot be ran on its own -- it needs to be integrated into a game engine.

If it happens at all, any further development of this project will most likely be done as a part of the **ngpe** game engine.

### Features

* Three-staged update: Emission, Motion, Appearance.
    * Emission - memory allocation (double buffer swap), particle spawn.
    * Motion - position and velocity update.
    * Appearance - color and size update.
* Expressions that are used to represent and calculate various parameters for each stage.
    * Similar to AST expressions; currently has no recursion.
* Can use either CPU or GPU for calculations.
    * GPU calculations were done using OpenGL compute shaders. Curently it means that GPU calculation support is only available for engines using OpenGL 4.3 or higher.
* Screen-space collision detection.
    * Uses depth and normal textures, thus is GPU-only.
* Creates vertex + index buffers (similar to [dear imgui](https://github.com/ocornut/imgui)) for particle rendering.
    * However, basically only relevant if CPU is used for the calculations.
* Tried out the AZDO style OpenGL API -- GPU rendering implementation uses bindless textures.

### Preview

Recordings of various particle effects ran in the **ngpe** engine using the Offbeat particle system.

![Particle effect live editing example](img/editing.gif)

![Fire](img/fire.gif)

![Smoke](img/smoke.gif)

![Waterfall colliding with a 3D mesh](img/waterfall_collision.gif)

![Hourglass](img/hourglass.gif)

![Sphere changing color depending on distance from camera (purple - orange)](img/purple_orange_sphere.gif)")

![Supernova-like explosion](img/supernova.gif)

![Flowy flames](img/flowy_flames.gif)

![Million particles (color changes depending on the distance from camera)](img/million.gif)

### Other notes

There are still plenty of things that could be implemented, fixed and experimented with:
* Sort particles by distance from camera (so that depth could be perceved properly).
* Add an option to change the quad facing direction. Currently quads can only face the camera.
* Change data layout to be SIMD friendly (to improve the performance on CPU).
* Try out cubemap depth/normal textures for (potentially) more accurate collision detection.
* Test the use of 3D meshes as particle emitters.
* Add a possibility to draw 3D meshes at the particle positions, not only 2D quads.
* Research and experiment with particle lighting and shadows.
* Vector fields.
* Lots of cleanup!

### Resources and references

* [The Destiny Particle Architecture](https://advances.realtimerendering.com/s2017/Destiny_Particle_Architecture_Siggraph_Advances_2017.pptx) ([SIGGRAPH 2017](https://advances.realtimerendering.com/s2017/index.html))
* [GDC Vault - Halo Reach Effects Tech](https://www.gdcvault.com/play/1014347/HALO-REACH-Effects)
* Jonathan Blow's particle system stream recordings: [1](https://www.youtube.com/watch?v=bFY-aOPnqEI), [2](https://www.youtube.com/watch?v=5c-mtq_WjaE), [3](https://www.youtube.com/watch?v=pAsFngEL8eI)
* Casey Muratori's Handmade Hero particle system episodes: [Day 155](https://guide.handmadehero.org/code/day155), [Day 156](https://guide.handmadehero.org/code/day156), [Day 336](https://guide.handmadehero.org/code/day336), [Day 337](https://guide.handmadehero.org/code/day337), [Day 338](https://guide.handmadehero.org/code/day338)
* [Shawn McGrath's rant](https://www.youtube.com/watch?v=q4nUK0EBzmI) (talks about various things, including particles)
* [GDC 2014 - AZDO in OpenGL](https://www.youtube.com/watch?v=K70QbvzB6II)
