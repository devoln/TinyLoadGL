# TinyLoadGL

A tiny single-header library to load OpenGL ES 2.0-3.2 core function pointers. Unlike most existing OpenGL function loaders, it doesn't expose any macros to the user. All loaded function pointers are contained in a struct.

Users can specify if they prefer static or dynamic loading.

The library just tries to load all the entry points it can find. It doesn't check if the GL version is actually supported. The user is responsible to check the OpenGL/OpenGL ES version and call only those functions available in that version.

## Usage

```cpp
#include <TinyLoadGL.h>
...

// static loading example (requires -lGLESv2)
constexpr auto gl = TinyLoadGL::Gles2Static;

// dynamic loading example
InitGLContextAndMakeItCurrent(); //using your windowing library like GLFW/SDL/platform-specific/etc.
const auto gl = TinyLoadGL::Gles2::Load(); //after an OpenGL context has been created
// or specify your own loading function:
const auto gl = TinyLoadGL::Gles2::Load(wglGetProcAddress);

// you can also force the library to load all the functions dynamically
const auto gl = TinyLoadGL::Gles2::LoadDynamic();

// Then call the functions without gl prefix
uint32_t prog = gl.CreateProgram();
//...
```

You can replace `Gles2` with `Gles3`, `Gles31`, or `Gles32` in the examples above to load the version you want.

## Dependencies

**None.**

The library doesn't require the user to include any other OpenGL-related headers and doesn't do it itself.

