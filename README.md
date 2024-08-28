# Ogre vcpkg Example Project

Getting started with Ogre on Windows using visual studio can be difficult!

You may find that there isn't a ton of helpful information available for issues you may run into while trying to get BasicTutorial1.cpp to compile.
There is a very comprehensive guide located at https://ogrecave.github.io/ogre/api/latest/tutorials.html but even this may not have everything you need to get Ogre up and running, especially if you're not used to the CMake build system.

While following the Ogre guide you may get down to the section titled [Installing and building via vcpkg](https://ogrecave.github.io/ogre/api/latest/building-ogre.html#autotoc_md273) and from there you may expect things to just work out. 

Spoiler: They won't.

This repository contains a pre-configured project that should have taken care of all of the necessary steps for getting your first project working with Ogre. 

Feel free to use this as a base for your future projects as well!

I strongly recommend compiling Ogre from source and using that rather than using the vcpkg version of Ogre. When I compiled this it was NOT up to date and after being setup it required much more work to actually get working properly. This project is the result of all the work I did and it's designed to get your project started quickly, but there's a strong chance that it'll make things easier in the future to just simply not use the vcpkg version.


# Usage

To start off with, this all assumes that you've installed Ogre using vcpkg. This can be done by opening Windows Terminal(or cmd) and entering the command:
```
vcpkg install ogre
```

If you don't have vcpkg added to your PATH environment variable, you'll have to open your Terminal to the directory where you installed vcpkg.

With Ogre installed via vcpkg, clone this repository and open the folder in Visual Studio. CMake should configure and you shouldn't run into any issues.

The project will have almost everything setup and ready to go right from the start. The exception to this is that you WILL need to edit [resources.cfg](https://github.com/NearEDGE/Ogre-vcpkg-Example-Project/blob/master/Ogre%20vcpkg%20example%20project/resources.cfg) and make it point to the folder containing Ogre's Media directory so that it can find ogrehead.mesh

You should follow the link above to have a look at it, but just in case here's how the file begins and a clear idea of what you need to do:
```
# Ogre Core Resources

# Important! Replace [OGRE MEDIA PARENT DIR] with the directory containing the Media folder in your Ogre installation from vcpkg
# This seems to be located at: %VCPKG_ROOT%/buildtrees/ogre/src/<version string>.clean/Samples
#

[OgreInternal]
FileSystem=[OGRE MEDIA PARENT DIR]/Media/Main
FileSystem=[OGRE MEDIA PARENT DIR]/Media/RTShaderLib
FileSystem=[OGRE MEDIA PARENT DIR]/Media/Terrain/

...
```

At time of writing, this directory was located for me at: `%VCPKG_ROOT%\buildtrees\ogre\src\v14.0.1-e1473b508d.clean\Samples\Media\models`

## Debugging

An important note is that the vcpkg version seems to be compiled using the `RelWithDebInfo` setting. What this means is that instead of selecting debug as your build configuration(Which isn't included in this project), you will need to select the build configuration I created named `x64 Release With Debug Info`. You will find this in the build configuration drop down next to the `Selected Startup Item` button (Which you may also know as the Debug button).

If you leave `x64 Release` selected, you will find that you can debug Ogre, but not your own application. 
This probably won't be particularly useful to you!
