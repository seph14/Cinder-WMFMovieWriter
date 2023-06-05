# Cinder-WMFMovieWriter
Simple movie recorder for Cinder using the Windows Media foundation.

This clocks was made by hacking [Tutorial: Using the Sink Writer to Encode Video](https://msdn.microsoft.com/en-us/library/windows/desktop/ff819477(v=vs.85).aspx). IT is not meant to be seen as a professional library nor will I be giving any kind of support.

For now it just writes h264 and WMV3 files, but you can modified it to suit your needs.
This fork added h265 support (but you need to have the HVEC plugin installed on your machine) and HardAccerlation option which fixes the compression issue with h265.

This fork only accepts Surface8uRef as the input and removed the support for texture2d.
Below is the sample code to add a surface:

```cpp
auto source		  = fbo->getColorTexture()->createSource();
auto constrain	= gl::SurfaceConstraintsGLTexture();
auto surf		    = Surface8u::create(source, constrain, true);
recorder->addFrame(*surf);
```
Where fbo has RGBA channels.

The WMF expects a unsigned char * array, so a surface is the perfect choice but if the data of a surface is passed, the color red a blue are swaped. 
The fastest solution found was to render to a FBO and swap the color in a shader.





