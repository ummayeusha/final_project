# Final_project

* **ID's:** Ummay Eusha (233003912), Miftahul Jannat (233016412)
* **Topic:** 2D Animated Windmill
* **Language:** C/C++
* **Graphics API:** OpenGL with GLU

## Project Overview

This repository contains a 2D computer graphics project built using C/C++ and the OpenGL/GLUT framework. The project simulates a rural landscape centered around a wind energy system. It features an animated rotating windmill, moving clouds across the sky, a power distribution house, residential structures, street lights with power cables, and surrounding vegetation.

This file provides a complete overview of the project's design, code structure, technical rendering mechanics, and potential practical uses.

## Key Features
* **Windmill Rotation:** Continuous rotation of the windmill blades driven by matrix transformations.
* **Cloud Animation:** Horizontal motion of clouds across the upper screen using timed coordinate updates.
* **Structured Scenery:** Rendering of a complete scene including a sky backdrop, green fields, a power house, houses, trees, and light posts.
* **Flicker-Free Display:** Double buffering enabled through GLUT to maintain smooth frame rendering during continuous updates.

## Technical Details and Code Logic
The project uses coordinate-based geometric primitives combined with transformation pipelines in OpenGL to build and animate the environment.

### 1. Primitive Shapes and Modules

* **Background (`background`)**: Sets up the scene canvas using `GL_QUADS` to divide the screen into an upper sky area and a full ground field, along with a road path extending toward the horizon.
* **Circle Generation (`drawCircle`)**: Since OpenGL lacks a built-in primitive for circles, a parametric circle function is defined using trigonometric functions (`sin` and `cos`). This helper is called repeatedly to form clouds (`cloud`) and foliage clusters (`tree`).
* **Structures (`leftHouse`, `powerHouse`, `lightPost`, `treeBase`)**: Architectural elements and infrastructure are built by layering quadrilaterals, triangles, and lines. Shading and color variations are managed through `glColor3f` calls to create depth between different faces.

### 2. Animation Mechanics

* **Rotational Transformation**: The windmill blades are rotated using matrix operations in `Display1()`:
glTranslatef(150.0f, 420.0f, 1.0f);
glRotatef(angle, 0.0f, 0.0f, 1.0f);
angle = angle - rate;
glTranslatef(-100.0f, -500.0f, -2.0f);

The pivot point is shifted to the hub of the windmill stand so the blades rotate around their center point frame by frame.

* **Linear Translation**: The horizontal movement of the clouds is handled in the `update()` timer function:
void update(int value) {
    posX += move_unit;
    if (posX > 1000) {
        posX -= 1000;
    }
    glutPostRedisplay();
    glutTimerFunc(50, update, 0);
}

## Practical Application and Context

This simulation visually demonstrates the basic working principle of wind energy generation and localized distribution:

1. **Harvesting Energy:** The kinetic energy of the wind turns the windmill blades.
2. **Power Processing:** Generated power is routed to an adjacent power station (`powerHouse`).
3. **Distribution Grid:** Power lines from light posts distribute electricity to nearby homes (`leftHouse`) and street lights.



## How to Build and Run
### Prerequisites

* GCC / G++ Compiler
* OpenGL development headers and GLUT libraries (`freeglut` or standard `glut`)

### Compilation
* **Windows (MinGW):**
g++ main.cpp -o windmill.exe -lfreeglut -lglu32 -lopengl32
./windmill.exe

## Output Preview

![Windmill Project Output](preview.jpg)
<img width="1327" height="850" alt="preview" src="https://github.com/user-attachments/assets/7f0840a7-17d8-49ba-b51e-ecab3e714804" />


This project demonstrates core 2D computer graphics principles including primitive assembly, custom shape generation via math functions, matrix transformations, coordinate translation, and frame rate management using GLUT timers. The result is a simple, structured 2D animation illustrating green energy conversion.
