Notes
    
    terms: 

    sdl - rendering library. handles window creation and has the functions which actually draw things to the screen
    byte - 8 bits. represents a number from 0-255
    memory - basically a big list of boxes containing a single byte each. 
             Each box can be thought of as having an index or address

    main memory - This is where all the data like variables and their values are stored.
                  For this program, main memory has 4096 bytes of which the first 512 are reserved for fonts/interpreter
                  Therefore we have (4096 - 512) bytes to work with as memory.

    register - special kind of memory seperate from main that belongs to the cpu.
               For this program there are 
                    16 general registers (named V0-V9 then VA, VB, .., VF). Each of these store 1 byte
                    index register (I) stores a memory address which some instructions use to store results
                    program counter (pc) stores the memory address of the  instuction in the instruction list that is being currently executed
                    stack pointer (sp) stores the index of the last address on the stack

                    Of these, VF is used to store flags

    flags - values that represent special events like "adding two numbers result in a carry over" or "subtracting two numbers resulted " etc.

    stack - memory seperate from main used to store certain locations in the instruction list where the program will need to go back to
            values in the stack are added and removed in Last-In First-Out order. 

    display - memory seperate from main that represents the screen.
              Here it is a list of 64*32 pixels. 
              Each pixel in display memory shows up as 10*10 screen pixels through the sdl rendering.

    instruction - something that the cpu should do.
                  for example, lets say there is two values A and B somewhere in memory we want to add.
                  to do this we need to load the values into any two registers then use an add instruction
                  the instructions would look something like:
                      load A V0      --take the value from A in memory and store it inside cpu register V0
                      load B V1
                      add  V0 V1 V2  -- add values in V0 and V1 and store the result in V2
                      store V2 C     -- store the value in V2 in a new place in memory called C

                  chip8 has 35 different instructions

    rom - read only memory. Here it is a text file which contains all the instructions as a list for the cpu to execute in order



    codebase:

        source files:

        1. chip8.cpp
            -all the cpu emulation stuff
            -important functions :
                initialize() -> initializes cpu by setting all memory, registers, stack, display to 0
                load_rom() -> reads the rom file into cpu main memory
                emulate_cycle() -> reads 16-bit instuction (opcode) and uses a big switch-case statement to handle each instruction then updates clocks

        2. main.cpp
            -contains the sdl code which uses the following functions:
                draw_graphics() -> checks every pixel in display memory and renders a white square to the correct pixels
                handle_input() -> checks if the keys that are being pressed are supposed to do anything
                audio_callback() -> contains the code to generate a beeping sound whenever required

            -contains main() where program starts and does the following:
                1. initialize sdl
                2. setup sdl audio device
                3. creates a window to render to
                4. creates a renderer
                5. calls the load_rom function
                6. starts a while loop which calls emulate_cycle 10 times each iteration and then updates the screen


        other files :

        1. chip8.h
            -header file which basically lists the variable and function names in chip8.cpp 
            -this file is to be included in main.cpp so it can use the names to reference the actual variables and functions in chip8.cpp

        2. main.o and chip8.o 
            -object files obtained after compiling main.cpp and chip8.cpp

        3. chip8
            -final executable obtained after linking main.o and chip8.o
            -takes one parameter which is the rom file from which the instruction list it to be grabbed


    tasks: 
        1. configure emulation speed
            - Use keyboard to increase/decrease cpu cycles per frame

        2. savestate 
            - save cpu attributes to a file or load them from file with keyboard ctls
    
        3. display color palettes
            - sdl stuff to change the colors through keyboard or menu
