# Photorealistic Teapot Using WebGL Project by Nicholas DaRosa
Github Page: https://ndarosa2.github.io/Photorealistic_Teapot/

Rotating Utah teapot that uses a combination of Lambertian diffuse reflection, Phong specular reflection, cylindrical texture mapping, procedure texture generation, bump mapping, and a spherical environment map to render an approximate photorealistic teapot. 

Geometry Processing: No changes were made versus the boilerplate code for geometry processing since the boilerplate code suffices as is. Boilerplate code follows traditional pipeline approach for geometry processing such as creating vertex buffer, coordinate space transformations,etc. 

Smooth Per-Pixel Shading: Followed the same methodology that was used in the Phong Shading assignment completed previously. The vertex position, normal vector (n), light vector (l), and view vector (v) from the vertex shader are sent to the fragment shader where those vectors are interpolated then renormalized.  These interpolated vectors are used in calculating the color of each fragment in the fragment shader. 

Diffuse Reflectance: Used Lambertian diffuse reflectance method with a single white light source. For the dot(n,l) calculation, n is the normal vector after bump mapping has been applied. 

Specular Highlights: Used the Phong specular reflectance method with white light and a specular gleam exponent of 10. For the reflect vector calculation, the normal vector after bump mapping has been applied was used. 

Surface Texture: Used cylindrical mapping for mapping surface textures. May be subtle, but surface texture is that of flycut metal which adds the appearance of swirls/archs to the surface of the teapot. Compared to source image, version used in this project has been brightened and color shifted. 
Source for flycut2.png texture: https://renderman.pixar.com/pixar-one-thirty   under Millmetals folder. 

Reflective Surface: Used a spherical environmental map of St. Peter's Basilica. Mapped texture coordinates s,t to the sphere map using the x and y components of the normal vector. This spherical environment map was considered part of the ambient light for the teapot. 
Source for St. Peter's Basilica probe (stpeters_probe.png): https://www.pauldebevec.com/Probes/

Procedural Texture: Created a procedural textural that places gold polka dots on the teapot. This was done in the fragment shader by taking each interpolated model vertex position, scaling that vertex positions by a factor of 15.0, then having the conditional statement that if the distance between the vertex position (x,y,z) and the vertex position rounded to the nearest integer is less than 0.18, then make that fragment the color of gold.

Bump Mapping: Created a black and white version of the illinois logo and slightly blurred it using online tools. Added this new black and white texture to the program as was done for the boilerplate textures except using gl.LUMINANCE instead gl.RGBA in the gl.texImage2D parameters. Then in the fragment shader, followed the methodolgy outlined in the course for bump mapping n' = n - dB/ds*(nxPt)+dB/dt *(nxPs) where n is the original normal, n' is the perturbed normal after bump mapping, dB/ds is the difference in luminance between adjecent fragments with respect to a small change in texture coordinate s,  dB/dt is the difference in luminance between adjecent fragments with respect to a small change in texture coordinate s, and Pt is dP/dt and Ps is dP/ds where P is a point on the teapot in terms of x,y,z. 
