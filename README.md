# DeSmuME-wasm

[WebAssembly port of the DeSmuME.](https://github.com/44670/desmume-wasm)

This fork is meant to add new debug log features, so that programmers can easily check what happens in their code avoiding stdio logic, which takes up code space and uses at least one background layer to be displayed (which is incommodating if your game visuals need all 4 layers of a screen).

# How it works

The Thumb instruction `mov r7,r7` is chosen as a breakpoint signal. That means, when that instruction is executed, the emulator prints out a message stored at the address refered by the `r6` register. 

Example of DS code:

```
  push {r6}
  ldr r6, =message 
  mov r7, r7
  pop {r6}

message:
    .ascii "Hello world from NDS logs!\n"
```

# How to build

You need CMake and Emscripten to be installed on your system.

Go to `desmume-wasm/` and execute the following commands:

```
mkdir build
cd build
emcmake cmake ..
emmake make
```
In the created `build` folder there should be two files: `nds.wasm`, `nds.js`. They are also available in the [releases](https://github.com/NotImplementedLife/desmume-wasm/releases/tag/build-wasm).

# Performance

Most 2D games could be run at 60fps on A14-based devices. 

However, the performance of 3D games varies for each game, an A15-based device could run most 3D games at nearly full speed.

By default, 30FPS limit mode is enabled. It is strongly recommended to enable this mode on A14-based devices (or earlier) to protect battery life and keep the temperature comfortable for playing. 

On A15-based devices, this mode could be disabled if you want to have a smoother experience.

# Control

Gamepads are supported if your OS supports it. Please note that iOS does not support most kind of gamepads, DualShock 4 is an officially supported one.

You may also want to control the game with a keyboard:
```
z: A
x: B
a: Y
s: X
q: L
w: R
enter: Start
space: Select
```
