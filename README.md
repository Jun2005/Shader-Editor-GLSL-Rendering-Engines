# Ray tracing and ray marching renderer from scratch using GLSL
Using self-taught knowledge on 3D rendering, I developed two distinct rendering engines using a mobile application called "Shader Editor". This application let's users write GLSL (OpenGL Shading Language) code and run the fragment shader program directly on their phone. Fragment shaders are programs written for the GPU that run individually for each pixel on the screen in parallel to determine the final color of the pixel.

## Ray tracing
<img src="https://github.com/user-attachments/assets/aa1a99fb-fb82-4916-a308-20a7233d2cb3" width="50%" />

The first rendering engine uses ray tracing which projects a ray for each pixel on the screen. It calculates the final color by considering the color, smoothness, and emissive property of the objects it collides with. A perfectly smooth object causes all rays to be specularly reflected where the angle of incidence is equal to the angle of reflection and the incident ray, normal direction and reflected ray are coplanar. On the otherhand, a rough object will cause the ray to be reflected in a random direction with a certain probability dependent on the roughness. To ensure an evenly distributed random direction, a random x, y, and z value is sampled from a normal distribution and it is normalized. The rendered image becomes less noisy and clearer overtime as the pixel color is calculated in each iteration and is averaged with the previous frame's result.

## Ray marching
This rendering engine takes a very different approach in rendering. It starts the same as ray tracing where a ray is projected for each pixel on the screen. However, instead of going straight to the point of collision, it takes small steps through the scene. It makes extensive use of Signed Distance Field (SDF) functions which returns the shortest distance to a geometric shape's surface given any point. In each iteration the ray takes a step in the ray direction with a distance equivalent to the value returned by the SDF function. This ensures that the ray will not collide with any geometry. It then repeats this step until a maximum number of iteration is reached or the SDF function returns a value smaller than a certain threshold value known as "epsilon". 

https://github.com/user-attachments/assets/a43f55ed-2d56-45a9-bb85-31cd27ab3452

This approach of rendering makes rendering infinite patterns and metaballs much easier by altering the SDF functions.

https://github.com/user-attachments/assets/1a95de80-881f-4af0-a49c-cef6354b909e

Very intricate infinite patterns can also be created by using noise functions as SDF functions. In the example above, a second ray march is performed using the noise SDF function if the initial ray march collided with the torus (ring shape) SDF. In addition, a second larger torus is rendered which uses voronoi noise to alter the direction of the normal to create the interesting light reflection patterns and the shape is outlined by considering the viewing angle and normal direction.

## Skills developed or gained
- Independent learning
- Problem solving: Graphics programming requires creative thinking and an unorthodox way of thinking which enhanced my problem solving skills.
- Greater attention and appreciation for optimization techniques: As the shader is run on a mobile device with very limited resources, greater care has to be taken to optimize the rendering engine.
