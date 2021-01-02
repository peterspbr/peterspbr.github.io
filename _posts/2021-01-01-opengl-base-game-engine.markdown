---
layout: post
title: "OpenGL base game engine"
date: "2021-01-01 22:46:39 -0200"
---

## Learning OpenGL by writing a game engine?
I'm new at OpenGL engines so i decided to head to a course and start learning. The course is very good but i decided to make something more interesting. I started to play with what i've already learned in the course (2D graphics) and i decided to make 3D graphics out of a simple white two dimensional triangle i've draw with **VAO**, **VBO** and **shaders** by myself.

### Man i need some better perspective...
By working with 2d graphics you are working with orthographic projection, and it doesn't combine with 3d graphics at all, so i started by using a method that i already learned before in my journey, that is using `glutPerspective()`. Well, as you can imagine it doesn't worked! So i headed to Internet and discovered that i no longer need to use it, i need to use glm.

Instead of this:
```c++
glMatrixMode(GL_PROJECTION);
glLoadIdendity();
glutPerspective(60.0f, double(windowWidth), double(windowHeight), 0.01f, 3000.0f);
glMatrixMode(GL_MODELVIEW);
glLoadIdendity();
```

I needed to use something a little more complicated.

I needed to create a `mat4` variable inside the fragment shader to make the projection then call `glm::perspective(glm::radians(60.0f), float(windowWidth) / float(windowHeight), 0.01f, 3000.0f);`

This looks more complicated in theory, but in practice is harder then that.

### Cordinates... why they are my nightmares...
If you already developed some application using OpenGL one thing you probably was pain with is vertices cordinates. That numbers that blow your mind and makes it feels like it will explode at any time. So i toke my mug of coffe and started **testing** all possibilities possible to make a simple cube. Yeah.. it can sound a little nobbie, but i done that.

I don't want anyone to pain. I'm a good guy
```c++
GLfloat vertices[] = {
    -1.0f, -1.0f, -1.0f,  0.0f, 0.0f,
     1.0f, -1.0f, -1.0f,  1.0f, 0.0f,
     1.0f,  1.0f, -1.0f,  1.0f, 1.0f,
     1.0f,  1.0f, -1.0f,  1.0f, 1.0f,
    -1.0f,  1.0f, -1.0f,  0.0f, 1.0f,
    -1.0f, -1.0f, -1.0f,  0.0f, 0.0f,

    -1.0f, -1.0f,  1.0f,  0.0f, 0.0f,
     1.0f, -1.0f,  1.0f,  1.0f, 0.0f,
     1.0f,  1.0f,  1.0f,  1.0f, 1.0f,
     1.0f,  1.0f,  1.0f,  1.0f, 1.0f,
    -1.0f,  1.0f,  1.0f,  0.0f, 1.0f,
    -1.0f, -1.0f,  1.0f,  0.0f, 0.0f,

    -1.0f,  1.0f,  1.0f,  1.0f, 0.0f,
    -1.0f,  1.0f, -1.0f,  1.0f, 1.0f,
    -1.0f, -1.0f, -1.0f,  0.0f, 1.0f,
    -1.0f, -1.0f, -1.0f,  0.0f, 1.0f,
    -1.0f, -1.0f,  1.0f,  0.0f, 0.0f,
    -1.0f,  1.0f,  1.0f,  1.0f, 0.0f,

     1.0f,  1.0f,  1.0f,  1.0f, 0.0f,
     1.0f,  1.0f, -1.0f,  1.0f, 1.0f,
     1.0f, -1.0f, -1.0f,  0.0f, 1.0f,
     1.0f, -1.0f, -1.0f,  0.0f, 1.0f,
     1.0f, -1.0f,  1.0f,  0.0f, 0.0f,
     1.0f,  1.0f,  1.0f,  1.0f, 0.0f,

    -1.0f, -1.0f, -1.0f,  0.0f, 1.0f,
     1.0f, -1.0f, -1.0f,  1.0f, 1.0f,
     1.0f, -1.0f,  1.0f,  1.0f, 0.0f,
     1.0f, -1.0f,  1.0f,  1.0f, 0.0f,
    -1.0f, -1.0f,  1.0f,  0.0f, 0.0f,
    -1.0f, -1.0f, -1.0f,  0.0f, 1.0f,

    -1.0f,  1.0f, -1.0f,  0.0f, 1.0f,
     1.0f,  1.0f, -1.0f,  1.0f, 1.0f,
     1.0f,  1.0f,  1.0f,  1.0f, 0.0f,
     1.0f,  1.0f,  1.0f,  1.0f, 0.0f,
    -1.0f,  1.0f,  1.0f,  0.0f, 0.0f,
    -1.0f,  1.0f, -1.0f,  0.0f, 1.0f
};
```

This is a little hard coded, but it works.

### Hxxppy conclusion
After some days (4 days) of pain, i finally make something visual and interactible! I post it in my [GitHub](https://github.com/peterspbr/opengl-game-engine) so go ahead and take a look! It's open-source!

#### Building
To build it is simple. If you are using Visual Studio Code you can simple run the default build task. But if not, you can bring up a terminal and write `g++ -o some-cool-name main.cpp -lGL -lGLU -lglfw`.

Enjoy!
