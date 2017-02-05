
This repository contains CMake scripts for finding the `SDL2`, `SDL2_image` and
`SDL2_ttf` libraries and headers.

CMake itself comes with corresponding scripts for SDL 1.2, which hopefully in
time will be updated for SDL2 and make this repo redundant. In the mean
time, I'm putting them up here in case anyone else finds them useful.

I've tested them on Linux and Mac OS using the Makefile and XCode targets.
On Linux, you'll need the SDL2 development packages installed from your distro
package manager. On Mac OS you can install the development frameworks
from the SDL website or alternatively, if you use Homebrew you can run
`brew install sdl2` to install the development packages.

##Usage

###General

In order to use these scripts, you first need to tell CMake where to find them, via
the `CMAKE_MODULE_PATH` variable. For example, if you put them in a
subdirectory called `cmake`, then in your root `CMakeLists.txt` add the line

```cmake
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${project_SOURCE_DIR}/cmake")
```

where `project` is the name of your project. You can then use the packages
themselves by adding

```cmake
find_package(SDL2 REQUIRED)
find_package(SDL2_image REQUIRED)
find_package(SDL2_ttf REQUIRED)

include_directories(${SDL2_INCLUDE_DIR}
                    ${SDL2_IMAGE_INCLUDE_DIR}
                    ${SDL2_TTF_INCLUDE_DIR})
target_link_libraries(target ${SDL2_LIBRARY}
                             ${SDL2_IMAGE_LIBRARIES}
                             ${SDL2_TTF_LIBRARIES})

```

or whatever is appropriate for your project.

###mingw32 / msys

This section supplements ```Usage -> General``` section. You still are required
to incorporate ```General``` configuration settings in you CMakeLists.txt.

Because cmake binaries for windows aren't aware of *nix/win paths conversion,
default paths FindSDL2 will look in won't do any good. For that you should set SDL2_PATH variable.
For example:
```cmake
set(SDL2_PATH "D:\\apps\\SDL2\\i686-w64-mingw32")
```

```bash
mkdir build
cd build
cmake .. -G"MSYS Makefiles"
make
```


##Licence

I am not the original author of these scripts. I found `FindSDL2.cmake`
after some Googling, and hacked up the `image` and `ttf` scripts from the
SDL1 versions that come with CMake. The original scripts, and my changes,
are released under the two-clause BSD licence.

##Bugs

These scripts are provided in the hope that you might find them useful. They
work for me and hopefully they'll work for you too. If you fix any
issues with them then I'd appreciate a pull request so other
users can get your fixes too, but that's up to you :-).


