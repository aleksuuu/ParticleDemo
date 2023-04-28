# Get Started With Unity’s Built-in Particle System

## Overview

The particle system simulates particle behavior on the CPU. The system and the particles can all be controlled by C# scripts, and using Unity’s physics system, the particles can interact with Colliders.[^1] It is commonly used to simulate clouds, flames, and other fluid or dynamic entities. There are two particle system solutions in Unity. The one discussed here is the Built-in Particle System, but more complex and large-scale effects can be achieved with the other solution, the Visual Effect Graph, which runs on the GPU.[^2]

The particle system is simply a component that can be added to any GameObject. As such, it comes with a number of properties that can be changed via the Inspector as well as through C# scripting. These properties are grouped into “modules” in the Inspector.[^3] While it is impractical to cover all of the available properties in this short guide, I will demonstrate the functions of the most important or useful ones with the following two examples.

## Example \#1:  Rain[^4]

Note: Some information about the properties comes from the Unity Manual.[^5] Any numeric values below can be altered to your liking.

1. Create a particle system by right-clicking in the Hierarchy and selecting Effect -> Particle System. Rename it to “Rain.” Reset the Transform.
2. In the Shape module, change the Shape property to Box. *The Shape property defines the shape of the emission volume. Hence when set to Box, particles will be emitted from the edge, surface, or body of a box shape, and they will move in the object’s forward (Z) direction.* In the Scale property, increase the X and Y values to 20. *This property defines the size of the emitter shape.*
3. In order for the particles to fall down, we need to provide a downward velocity. Enable the Velocity over Lifetime module. Click on the triangle to the right of the Linear fields, and select Random Between Two Constants. *Note that most numeric fields in the Particle System component can be randomized this way to create a more natural effect.* Then, change the first (top) Linear Y value to -25, and the second (bottom) Linear Y value to -35. *The Linear”X, Y, and Z values are the linear velocity of particles in the X, Y and Z axes.*
4. In the Renderer module, change the Rendering Mode to Stretched Billboard, so that the particles can be stretched in a direction we specify. 
5. Back to the Main module (the very first module before Emission), enable 3D Start Size as raindrops would have different sizes on each axis. Again, through the triangle to the right, select Random Between Two Constants. Change both X values to 0.1, the first Y value to 1, and the second Y value to 2, and both Z values to 0.1. 
6. 



[^1]: https://docs.unity3d.com/Manual/Built-inParticleSystem.html
[^2]: https://docs.unity3d.com/Manual/ChoosingYourParticleSystem.html
[^3]: https://docs.unity3d.com/Manual/class-ParticleSystem.html
[^4]: https://www.youtube.com/watch?v=SrWrUN56UWU
[^5]: https://docs.unity3d.com/Manual/ParticleSystemModules.html
[^6]: https://www.youtube.com/watch?v=UllkvfMR96s



