# seam-carver
#### Work in progress!
OpenCV4 based utility for **efficient** content-aware scaling.
Includes a basic wrapper for user control but the main focus is on the underlying `Carver` class which is used for the actual image processing. 
Feel free to add any GUI bindings or an advanced CLI for easy usage.

Basic usage:

```carver -m <mode> -o <output_path> <input_path>```

#### How does it work?
[Wikipedia](https://en.wikipedia.org/wiki/Seam_carving) includes a decent explanation on the topic. The basic idea is to 
pick a method to assign an importance value to each pixel and then locate the least important seams through the image. This
solution uses gradient magnitude (energy) as the importance value. Energies are updated each time a seam has been cut from 
the image to achieve best possible quality.

Asynchronous C++ threading and  OpenMP are both used for better performance. These features can be disabled by removing the define:

```#define CONCURRENT```

Processing small images is quite swift but bear in mind that the actual complexity of this algorithm is in the range of

![image](https://latex.codecogs.com/gif.latex?O%28W%24%5Ctimes%24H&plus;W&plus;H%29)

#### How to get it?
If you want to use this as a standalone program instead of including the code as part of your own project **cmake** is the recommended workflow.
If you do not feel like building, some premade binaries will be attached to releases. Dependencies for the dynamically linked binaries are:

```
libopencv_imgcodecs.so.4.3
libopencv_imgproc.so.4.3 
libopencv_core.so.4.3 
libgomp.so.1 
libpthread.so.0 
libstdc++.so.6 
libgcc_s.so.1 
libc.so.6 
libpng16.so.16 
libz.so.1 
libm.so.6 
libdl.so.2 
```

#### Example output when running in vertical mode
![image](https://user-images.githubusercontent.com/36196504/80315324-72c2ca00-87ff-11ea-97c0-80c9b8d8c2aa.jpg)
![image](https://user-images.githubusercontent.com/36196504/80315328-77877e00-87ff-11ea-939c-c01988cc9c9d.jpg)
