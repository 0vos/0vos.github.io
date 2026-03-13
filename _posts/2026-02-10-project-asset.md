---
layout: single
title: "Physics-Enabled 3D Asset Library for Robotic Simulation"
date: 2026-02-10
permalink: /project-asset/
categories:
  - Projects
excerpt: "A robust 3D asset library built in Unity for robotic arm tasks, featuring precise colliders, articulated assembly, and AI-generated models."
header:
  teaser: "assets/images/PA.jpg" 
---
This project provides a physical 3D model asset library for robotic arm data collection. Specifically, it is mainly divided into the following parts:

1. Placement of simple convex objects
2. Assembly of colliders for concave objects
3. Assembly of articulated objects
4. Generation of 3D objects

We initially used Swift's native 3D animation system, but it had two problems: first, the lighting reflection was very strange, causing some faces of the object to display properly while others appeared completely white; second, the composite colliders formed by assembling simple colliders constantly jittered on the desk, and no matter how many preventive measures were added, it could not be stopped.

Obviously, the second problem is fatal in the field of robotics simulation. SceneKit's collision only has three forms: boundingBox, concavePolyhedron, and convexHull. Among them, boundingBox is the most accurate, but having only a cubic collider is definitely insufficient for a robotic arm's pick and place tasks; concavePolyhedron should theoretically meet the collision requirements of concave objects (like bowls), but it can only be applied to static objects, and its support for collision accuracy is not very high (it causes clipping); convexHull can give objects a convex collider, but for some unknown reason, the object's collider seems to always be larger than the visual body, and no matter how we adjust it, we could not build a minimal convex collider.

Therefore, we had no choice but to switch to an engine with more mature animation and physics systems like Unity (although it is mostly used for making games). Facts have proved that the many problems encountered in SceneKit above were quickly solved in Unity's animation system. Moreover, in Unity, making objects click-to-place and continuously tracking their positions only requires attaching a C# script to the object in the scene, which is very convenient.

For the assembly of colliders for concave objects, since the xml files for Mujoco are written very clearly, the position, rotation, and size of each collider block can be easily obtained; we only need to place the collision blocks at different positions according to the Mujoco file and then combine them together.

<div style="text-align: center; margin-bottom: 1em;">
  <div style="position: relative; padding-bottom: 56.25%;   height: 0; overflow: hidden; border-radius: 8px;  margin-bottom: 1em;">
    <iframe 
      src="https://www.youtube.com/embed/lBdWdc6Gf84? autoplay=1&mute=1&loop=1&playlist=lBdWdc6Gf84& controls=0&rel=0" 
      style="position: absolute; top: 0; left: 0; width:  100%; height: 100%; border: 0;" 
      allow="accelerometer; autoplay; clipboard-write;  encrypted-media; gyroscope; picture-in-picture" 
      allowfullscreen>
    </iframe>
  </div>
</div>

For articulated objects, we chose SAPIEN's articulated objects for assembly. The principle of assembly is similar to the assembly of composite colliders, but this time it involves parsing URDF files.

Finally, to adapt to complex task environments in reality, I added Rodin API for 3D model generation (which is relatively accurate in physical structure and basically reasonable in textures), and the generated models are processed as simple concave objects.