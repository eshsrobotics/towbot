# towbot
Raspberry Pi + Arduino + elbow grease = T.O.W.B.O.T.: The Obviously Worked-on Bot Of 'Taters (working title)


The Towbots are a group of three robots designed to follow vision targets with a camera, while at the same time carrying a dead load (hence "tow" bots.) The Towbots are explicitly intended to be able to follow one another, or to follow anyone or anything that is holding a suitable vision target within the Towbot's field of view.

This is an extracurricular project that will help to sharpen the programming skills of the P.O.T.A.T.O.E.S. team while hopefully being fun to work on.

## Installation instructions
1. First, install the OpenCV development library.  How you do that will vary
   from platform to platform.
   * Here's how it's done on Ubuntu:
        sudo apt-get install libopencv-dev libopencv-contrib-dev
   * On OSX, using `homebrew`:
        brew install opencv
### C++ build instructions
1. Install `cmake` by whatever means you prefer.
1. ArUco has some optional dependencies that we don't strictly need:
   1. `doxygen` -- needed only to run `make doc`, should you want to generate
      local ArUco API documentation.
   1. `libglut-devel` -- needed only to build some of ArUco's utility
      programs.
1. To generate the `Makefile`, execute the following command from the
   project's base directory:
    ``` shell
    cmake .
    ```
    If you prefer an interactive configuration, use `ccmake .` or the
    CMake-GUI instead.
1. Build the actual code using the `Makefile`.  Note that it will actually
   build the nested `aruco` codebase, so it may take a while the first time it
   is run.
   ``` shell
   make
   ```
   * If you are using the Raspberry Pi, I **strongly suggest** you build with
     the following command instead:
     ``` shell
     nice -n 19 make
     ```
     This will prevent the build from overheating the CPU and causing the
     Raspberry Pi to crash.

#### How to use the `calibrate` utility
In addition to the other programs built by this project, you will find an
OpenCV utility called `bin/calibrate`.  Its purpose is to analyze special
**pattern images** taken from a camera, deduce the critical parameters needed
to undo the camera's lens distortion, and write these parameters to an output
file.  It can take its image data from a live camera feed, a recorded video
file, or a series of photograph snapshots, depending on what its input XML
file specifies.

The `calibrate` program requires X (*which is somewhat nonsensical, given that
X is only used to display intermediate image data--we may change this
later*).  On Cygwin, you must install the `xorg-server` and `dbus` packages.

To see how `calibrate` works in practice, try one of these commands:

     bin/calibrate.exe samples/calibration/with-images/settings.xml

The program will wait for keyboard input on the X display--just hit `space` or
`enter`.  In the end, it will generate a file called `out_camera_data.xml`
containing the calibration parameters.

#### Helpful tools
To take pictures and record video with the Logitech webcams, a number
of tools are available.  On Linux, we have used `cheese` with some
degree of succcess.  Search for similar tools with `apt-cache search
webcam`.

### Python build instructions
1. Install this project's local Python dependency packages as follows:
    pip3 install --user -r requirements.txt
