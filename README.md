# Get started with Unity’s built-in Particle System

## Overview

The particle system simulates particle behavior on the CPU. The system and the particles can all be controlled by C# scripts, and using Unity’s physics system, the particles can interact with Colliders.[^1] It is commonly used to simulate clouds, flames, and other fluid or dynamic entities. There are two particle system solutions in Unity. The one discussed here is the Built-in Particle System, but more complex and large-scale effects can be achieved with the other solution, the Visual Effect Graph, which runs on the GPU.[^2]

The particle system is simply a component that can be added to any GameObject. As such, it comes with a number of properties that can be changed via the Inspector as well as through C# scripting. These properties are grouped into “modules” in the Inspector.[^3] While it is impractical to cover all of the available properties in this short guide, I will demonstrate the functions of the most important or useful ones with the following two examples.

## Example \#1:  Rain

Note: This tutorial is largely based on [SpeedTutor](https://www.youtube.com/@SpeedTutor)’s YouTube video.[^4] Some information about the properties also comes from the Unity Manual.[^5] Any numeric values below can be altered to your liking.

### Creating raindrops

1. Create a particle system by right-clicking in the Hierarchy and selecting Effect -> Particle System. Rename it to “Rain.” Reset the Transform. Since we are emulating rainfall, it might be a good idea to increase the Transform Y value. 
2. In the Shape module, change the Shape property to Box. *The Shape property defines the shape of the emission volume. Hence when set to Box, particles will be emitted from the edge, surface, or body of a box shape, and they will move in the object’s forward (Z) direction.* In the Scale property, increase the X and Y values to 20. *This property defines the size of the emitter shape.*
3. In the Emission module, increase the Rate over Time to 100 to increase the number of raindrops present at any moment. *This property controls the number of particles emitted per unit of time. Note that this rate is independent of the size of the emitter; therefore, enlarging the emitter could spread out the raindrops.* 
4. In order for the particles to fall down, we need to provide a downward velocity. Enable the Velocity over Lifetime module. Click on the triangle to the right of the Linear fields, and select Random Between Two Constants. *Note that most numeric fields in the Particle System component can be randomized this way to create a more natural effect.* Then, change the first (top) Linear Y value to -25, and the second (bottom) Linear Y value to -35. *The Linear”X, Y, and Z values are the linear velocity of particles in the X, Y and Z axes.*
5. In the Renderer module, change the Rendering Mode to Stretched Billboard, so that the particles can be stretched in a direction we specify. 
6. Back to the Main module (the very first module before Emission), enable 3D Start Size as raindrops would have different sizes on each axis. Again, through the triangle to the right, select Random Between Two Constants. Change both X values to 0.1, the first Y value to 1, and the second Y value to 2, and both Z values to 0.1. 
7. In the Main module, set the Start Speed to 0, as the velocity is controlled by the Velocity over Life time module.
8. In the Main module, adjust the Start Lifetime according to how high the emitter is relative to the ground. The higher the emitter, the longer the lifetime needs to be so that the particles would reach the ground.
9. In the Main module, lower the alpha value of the Start Color by half, so that the raindrops appear more translucent.
10. To fade in and out the raindrops, enable the Color over Lifetime module. *The very left-hand point of the gradient bar indicates the beginning of the particle’s life, and the very right-hand side of the gradient bar indicates the end of the particle’s life. The points above the gradient bar indicate alpha values, and the ones below indicate colors. More points can be added by clicking above or below the gradient bar.* Change the starting and ending points above the gradient bar to 0 so that the raindrops start with an alpha value of 0. Then, add two points above the gradient bar, one slightly to the right of the starting point and another slightly to the left of the ending point. Keep both alpha values at 255. *Note that this property blends with the Start Color property.*
11. Enable the Collision module. When the Type property is set to World, the particles would collide with any Collider in the scene. Now the raindrops should bounce off the ground, but that is not what we want. Therefore, set the Dampen property to 1, Bounce to 0, and Lifetime Loss to 0.5. *Dampen determines the fraction of a particle’s speed that it loses after a collision (hence when set to 1, the particle is stopped after a collision); Bounce determines the fraction of a particle’s speed that rebounds from a surface after a collision (hence when set to 0, the particle does not rebound at all); Lifetime Loss determines the fraction of a particle’s total lifetime that it loses if it collides (hence when set to 0.5, the particle’s lifetime is cut by half).*

### Creating splashes (using Sub Emitters)

To create more convincing raindrops, we could add some splashes when the rain hits the ground using another Particle System that is automatically spawned.

1. Enable the Sub Emitters module. In the drop-down menu, change the condition to Collision. Then, add a sub Particle System by clicking on the “+” on the right. A new child object of the Rain GameObject would be created. Rename it to Splash.
2. We will use an unfilled circle with a white border to create a texture for the splashes. You could simply create this shape with the following SVG code and convert it to PNG.

`
<svg width="200" height="200">
  <circle cx="100" cy="100" r="50" stroke="#ffffff" stroke-width="2" fill="none"/>
</svg>
`

3. Import the circle into the Assets folder. In the Inspector, check the Alpha Is Transparency box.
4. Create a new Material, and rename it Splash. Change the Shader to Particles/Standard Unlit. Change the Rendering Mode to Fade. *This allows the transparency values to entirely fade an object out, including any specular highlights or reflections it may have.* Drag the circle PNG file from the Assets folder to the Albedo map of the new material. Lower the alpha value to about 190.
5. Go back to the Splash sub Particle System object. In the Renderer component, apply the newly created Splash material to the Material property. Set the Render Mode to Horizontal Billboard as the splashes should appear on the floor horizontally.
6. In the Main component of the Splash object, lower the Start Lifetime to 2 so that the splashes disappear sooner. Change the Start Speed to 0 so that the splashes do not move when they are being created.
7. In the Emission component, lower the Bursts’ Count to 1. *A burst is an event which spawns particles. A Count of 1 means every collision between a raindrop and the ground would only spawn one splash.*
8. Enable the Color over Lifetime module. Follow step 10 of the [section above](#creating-raindrops) to fade in and out the splashes.
9. To make the splashes grow over time, enable the Size over Lifetime module. The default curve (a linear slope growing from 0.0 to 1.0) should work.
10. If the particles are too small, adjust Scale in the Transform.

[^1]: https://docs.unity3d.com/Manual/Built-inParticleSystem.html
[^2]: https://docs.unity3d.com/Manual/ChoosingYourParticleSystem.html
[^3]: https://docs.unity3d.com/Manual/class-ParticleSystem.html
[^4]: https://www.youtube.com/watch?v=UllkvfMR96s
[^5]: https://docs.unity3d.com/Manual/ParticleSystemModules.html
[^6]: https://www.youtube.com/watch?v=SrWrUN56UWU



