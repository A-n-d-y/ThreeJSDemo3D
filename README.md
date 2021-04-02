# ThreeJSDemo3D


## [View the Demo](https://three-js-demo-3d.s3.us-east-2.amazonaws.com/index.html)

![enter image description here](https://i.ibb.co/rs21cKG/threejs.png)
# Overview
**This one day project was my first introduction into three.js, with the aim to explore how 3D rendering works within the framework.**

My aim was to:
 - Research configuration and setup
 - Create a 3D environment in three.js
 - Add some form of interactivity/motion/animation
 - Host a demo of the page


## Step 1 - Research configuration and setup
Set up was pretty straight forward. 

To test locally, I ran a node.js server with:
`npm install http-server -g`
`http-server .  -p 8000`

As I've been using Unity for a number of years, I am familiar with the concepts on how three.js works (Camera, scenes, renderers etc.) To expedite the development of the scene, I looked into creating this in Unity and importing it into three.js.
I noticed 2 plugins on the Unity asset store to achieve this. I had no luck with these, so I constructed the scene in Three.js.


## Step 2 - Create a 3D environment in three.js
Regarding the assets, I struggled with importing .obj and .fbx as I had trouble with the materials. After a bit of research, the optimal format appears to be glTF (GL Transmission Format). This format is compact for loading times and focuses on runtime asset delivery. I opted for this [asset pack](https://opengameart.org/content/retro-urban-kit) from [Kenny](https://opengameart.org/users/kenney). 
On reflection, I could have looked further into exporting scene content as glTF from Unity or blender, but this is ultimate counter-intuitive to investigating a technology that I am unfamiliar with, and it would have wasted time, given I had a day.

I don't think I'll be switching to Three.JS anytime soon to construct 3D environments; It wasn't a quick process. The Three.JS Editor was very useful, but as you'd expect, it can not compete with the functionality of Unity's scene editor. I'd personally prefer to look into [Unity Instant Games](https://unity.com/solutions/instant-games) to achieve instant WebGL loading for 3D scenes and games. I wasn't able to move throughout the scene without focusing on an object first, and no shortcut key to clone an object. I think these two things would have really helped out. The [source code is available here](https://github.com/mrdoob/three.js/tree/master/editor/js), so I think I'll look into creating a pull request for the shortcut key before commencing with further work.

## Step 3 - Add some form of interactivity/motion/animation
My original plan was to have interactive street lighting and an animated vehicle following a spline. This proved too ambitious, due to the length of time required to create the scene. 
I focussed on an animated vehicle. I wanted the vehicle to follow a curve to handle corners gracefully, along with using a tween library so the speed would adapt depending on the position on the road. 
Unfortunately I settled on a quick solution, where the position and rotation are dictated by vector positions of the road. An example of this is below:

    if (this.position.z <= 6.369 && this.position.x >= 0.47)
    {
    	this.position.z += 0.05
    	this.rotation.y = 0
    } else if (this.position.z > 0 && this.position.x <= -8.5)
    {
    	this.position.z -= 0.05
    	this.rotation.y = 3.14159
    }

## Step 4 - Host a demo of the page
I kept this simple as it doesn't require anything significant, so opted to host from an AWS S3 bucket.

## Remaining tasks
 Although this isn't something I'll jump back into anytime soon, I'd like to allocate another day to polish things up a bit. I'd aim to:
 - Finish the scene (Only 2 sides of the street were completed)
 - Add a skybox
 - Add a spline for the vehicle to follow, along with smooth cornering 
 - Adjustable speed of the vehicle from the webpage
 - Street lighting
 - General polishing of the scene, maybe a nice shader on the camera

## Conclusion
 While I didn't make as much progress as I'd like in a day, I am impressed with what can be achieved with the Javascript 3D library. I wouldn't be starting new projects with three.js any time soon, but I'm confident I'll encounter a situation where three.js may be the well suited to the project requirements. 
