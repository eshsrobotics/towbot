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
1. To generate the `Makefile`, execute the following command from the
project's base directory:
    cmake ./build
1. Build the actual code using the `Makefile`.  Note that it will actually build the nested `aruco` codebase, so it may take a while the first time it is run.
    make
### Python build instructions
1. Install this project's local Python dependency packages as follows:
    pip3 install --user -r requirements.txt
