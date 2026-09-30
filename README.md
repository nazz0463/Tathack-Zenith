
Chip 8 Emulator
Tathack-26

Team Zenith :
  Haazim 
  Yaseen
  Nazil 
  Joshua

Problem Statement:
  You are given a partially completed CHIP-8 emulator codebase in C++ using SDL2. While the foundation is present, the codebase contains intentional implementation bugs that degrade timing, screen rendering, opcode processing, and input management.
  Your primary objective is to debug the existing core, stabilize execution across standard CHIP-8 ROMs, and extend the system with innovative feature additions.

Bugs found :
  1.Error in returning from a subroutine
  2.Incorrect timing in main loop
  3.Flipped display
  4.Incorrect handling for certain instructions

Feature Extension
Following additions were made
Configurable Emulation Speed: Added keyboard controls to dynamically increase or decrease CPU clock cycles per frame during runtime.
Savestate Management: Implemented state saving and loading (save emulator memory, registers, PC, stack, and timers to a file and restore on keypress).
Custom Display Color Schemes: Implemented configurable display colors
