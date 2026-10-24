# Mukbo DB (2011)

A small Windows console game written in C++. The Korean title, 먹보DB, means "DB the glutton". You steer the hero "DB" (drawn with the `㏈` character) through a walled map with the arrow keys and eat every piece of bread (`Θ`). Each piece adds 5 g to DB's weight, and the screen shows the total bread, the bread eaten, DB's weight and the turn count. When the last piece is gone, a victory screen shows the number of turns and the final weight. The title screen, the stage-select screen and the victory screen are drawn with box-drawing characters, and `p` quits during play. The screens are in Korean.

## Background

- Year: 2011.
- Made alone by Dawn as a university course project: assignment 4 of an object-oriented programming course.
- The title screen credits ㈜BNItech as the maker.

## What the code does and does not do

The course report planned more than the code contains. What is in `main.cpp`:

- title screen (1 to start, 2 to quit) and a stage-select screen that accepts any digit from 0 to 9 but says the stages are still being prepared
- one map, arrow-key movement with wall collision, eating bread, weight and turn counters
- the victory screen

Not implemented: monsters, the "overeater" transformation (its status line is always printed as `off`), real stage selection, and replay (choosing "try again" on the victory screen shows the title screen and then the victory screen again instead of resetting the map).

## Build and run (Windows)

The code uses `conio.h` and the Win32 console API, so it builds only on Windows. It was written for Visual C++ 2008 as a precompiled-header console project, so it includes `stdafx.h`; create an empty one next to `main.cpp` first.

Visual Studio 2015 Update 2 or newer (the first version with `/execution-charset`), from a Developer Command Prompt:

```bat
type nul > stdafx.h
cl /EHsc /execution-charset:.949 main.cpp
chcp 949
main.exe
```

MinGW-w64 (g++):

```bat
type nul > stdafx.h
g++ -std=c++98 -fexec-charset=CP949 main.cpp -o mukbo.exe
chcp 949
mukbo.exe
```

The screens are laid out for the Korean console code page (949), where Korean letters and box-drawing characters are two columns wide. The `/execution-charset:.949` and `-fexec-charset=CP949` options store the text in that code page, and `chcp 949` switches the console to it. These commands were not tested for this release (no Windows machine was available); the source was only checked for syntax with stand-in headers.

## Changes for this public release

- The source was a single text file in the Korean CP949 encoding. It is now `main.cpp` in UTF-8 (with a byte-order mark, so Visual C++ reads it as UTF-8 without extra options).
- One stage name on the stage-select screen was a real person's name used as a joke. It was replaced with the neutral word 천재 ("genius"), padded so the box keeps its width. Nothing else in the code was changed.
- Left out: the original assignment archive and report (they contain personal and course details), the course's template files, and a scratch list file.

## Licence

MIT, see [LICENSE](LICENSE).

The two helper functions `gotoxy()` and `clrscr()` follow code provided in the course and are not covered by the licence.

## Status

Partial: playable from start to victory on one map, but monsters, stage selection and replay were never finished.
