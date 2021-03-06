#ARBaseLib
A modified version of the ARBaseLib of the ARToolKit Android SDK for use in marker tracking and surface rendering.

##Synopsis
This project extends the capabilities of the ARBaseLib by including new packages for `readers` and `rendering`.

##Motivation
The goal of this project is to develop a head mounted display (HMD) for surgeons to use as a navigational aid during a procedure.
The Wearable Intelligent Navigation System for Surgery (WINSS) Augmented Reality (AR) system allows for image guided surgery without the need to occupy a surgeon’s hands or eyes. 
Rather than providing high-resolution preoperative images, the HMD will show derived graphics and models, 
such as tumor outlines and target points in a “picture in picture” manner, to assist in navigation. 
By using the AR device in conjunction with other sensors for optical tracking and inertial sensing, 
the system can operate even when markers on the patient frame are occluded from the view of a tracker. 

##Installation and Testing
This project is a modified version of the [ARBaseLib package](https://github.com/artoolkit/artoolkit5/tree/master/EclipseProjects/ARBaseLib) 
of ARToolKit.
After compiling the ARBaseLib package, this project can be used as an Android Library for use in other applications.

The Android version of the ARToolKit SDK is implemented using a Java wrapper around native C++ code, compiled using the Java Native Interface (JNI).

The application was built and tested on the [Epson Moverio BT-200 smart glasses](http://www.epson.com/cgi-bin/Store/jsp/Landing/moverio-bt-200-smart-glasses.do?ref=van_moverio_2014).

##Code Example
The following packages were added to the ARBaseLib project to extend the functionality of this library.

####`org.artoolkit.ar.base.rendering`
The `ARRenderer` and `RenderUtils` classes were found in the original source. All other classes are new.

The `rendering` package contains the general representation of a surface that can be rendered along with some sample shapes.
The `Shape` abstract class defines the elements needed to render a surface, namely a collection of points defined by coordinates, 
the indices of each point that defines a face of the surface, and an array of colors corresponding to each point.
In addition, every shape can be transformed by rotations around the x, y, and z axes, translation, and scaling using methods defined in the `Shape` class.
Certain implementations of the `Shape` class, specifically, `STLSurface` parse files to construct the renderings.

####`org.artoolkit.ar.base.readers`
The `readers` package contains the classes needed to parse a file into the format used by ARToolKit. The `SurfaceReader` abstract class
provides a generalization of a reader, with subclasses implementing these methods for specific file types. 
`STLReader` is an implementation of this class specific to the [STL file format](https://en.wikipedia.org/wiki/STL_(file_format)).

Notes:
* This reader can be constructed with either a `String` of the file name or an `InputStream`, but for Android applications it is recommended to use the latter.
* `STLReader`'s expect the surface to be made up of triangular facets, that is to say each facet has three vertices

####STL Surfaces
STL models can be read from a `.stl` file in an Android project's `assets` folder. 
When initalized, `STLSurface` objects use `STLReader`'s to parse the file and create a model.

**How to construct an `STLSurface` in an `Activity`:**
```java
InputStream is = this.getAssets().open("stl_file.stl");
STLSurface sur = new STLSurface(is);
```

##API Reference
The ARToolKit library can be found at http://artoolkit.org/ with the [original documentation](http://artoolkit.org/documentation/).

All code added to this library is documented in `Javadoc` format.

`.pdf` and `.png` versions of all available markers can be found in `ARBaseLib/doc/patterns`.

##Contributors
This project was made possible with support from Dr. Peter Kazanzides and Dr. Sungmin Kim
of the Laboratory of Computational Sensing and Robotics at Johns Hopkins University.
