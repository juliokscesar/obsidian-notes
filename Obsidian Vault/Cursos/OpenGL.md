[LearnOpenGL](https://learnopengl.com/)
# Basic Concepts
## Immediate Mode vs Core-Profile
In the old days, OpenGL was used by developing in immediate mode, which means that the response from the request made to the GPU works linked directly with your program's flow (for example, specifying a triangle to be drawn between `glBegin` and `glEnd`. This is slow and inefficient.  Also, it abstracted a lot of operations and did not allow much control over how OpenGL operates.

Core-profile is faster and forces us to use modern practice. It allows the GPU to work faster with for example Vertex Buffer Objects (VBO). Although it is more difficult.

## OpenGL versions
This course uses OpenGL 3.3. The reason to not use more updated versions (like 4.6+) is because after 3.3 it only adds extra useful features without changing it's core mechanics. Also, recent versions of OpenGL requires recent graphics cards, leaving oldish systems behind.

## Extensions
Whenever a graphics company comes up with a new technique or a new large optimization for rendering it is often found in an extension implemented in the drivers.


## State machine (Context)
OpenGL is by itself a large state machine. A collection of variables define how OpenGL should currently operate in the given context.
The common approach to using OpenGL is changing its state by setting some options, manipulating some buffers and then render using the current context.

## Objects
Since OpenGL libraries are written in C, a lot of abstractions are made through *objects* (not OOP, but like struct objects).
An object in OpenGL is a collection of options that represents a subset of OpenGL's state.

The OpenGL's context itself can be thought as a object, like:
```cpp
struct OpenGL_Context {
	object_name* object_window_target;
}

// Then to use objects:
unsigned int objectId = 0;
glGenObject(1, &objectId);
// bind/assign object to context
glBindObject(GL_WINDOW_TARGET, objectId);
// set options of object currently bound to GL_WINDOW_TARGET
glSetObjectOption(GL_WINDOW_TARGET, GL_OPTION_WINDOW_WIDTH, 800);
glSetObjectOption(GL_WINDOW_TARGET, GL_OPTION_WINDOW_HEIGHT, 600);
// set context target back to default
glBindObject(GL_WINDOW_TARGET, 0);
```
This code is an example of workflow with OpenGL context and objects. 

## GLFW
GLFW is a library written in C specifically targeted at OpenGL. It allows us to create an OpenGL context, define window parameters, and handle user input.
It is necessary because, without it, most operations involving OpenGL are OS specific, and GLFW helps to minimize this work.

**Using GLFW (Linux)**:
OpenGL libraries are downloaded with the graphics driver and GLFW can be downloaded through pack manager.
It is also possible to download GLFW through their site to include the files in the project folder directly too.
When building, these are the libraries to add with GCC:
`-lglfw3 -lGL -lX11 -lpthread -lXrandr -lXi -ldl`

## GLAD
Because OpenGL is only really a standard/specification it is up to the driver manufacturer to implement the specification to a driver. Since there are many versions of OpenGL drivers, the location of most of its functions is not known at compile-time and needs to be queried at run-time. Retrieving those locations is OS specific.
GLAD is an open source library that manages that.

# Basic window creation code
```cpp
// GLAD must always be included before any other header files that use OpenGL
#include <glad/glad.h>
#include <GLFW/glfw3.h>

#include <iostream>

void framebuffer_resize_callback(GLFWwindow* window, int width, int height);

int main()
{
	glfwInit();
	
	// Set OpenGL version 3.3 to be used
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);

	// Set Core-profile to be used
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);
	
	int WINDOW_WIDTH = 800;
	int WINDOW_HEIGHT = 600;
	// Create Window object
	GLFWwindow* window = glfwCreateWindow(WINDOW_WIDTH, WINDOW_HEIGHT, "Hello World!", nullptr, nullptr);
	if (!window)
	{
		std::cout << "Failed to create GLFW window\n";
		glfwTerminate();
		return -1;
	}

	// Set current context to this window
	glfwMakeContextCurrent(window);

  

	// Initialize GLAD
	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress))
	{
		std::cout << "Failed to initialize GLAD\n";
		return -1;
	}
	
	// Set viewport size (rendering window)
	glViewport(0, 0, WINDOW_WIDTH, WINDOW_HEIGHT);
	// set callback for when user resizes window
	glfwSetFramebufferSizeCallback(window, framebuffer_resize_callback);
	
	// Initialize program loop
	while (!glfwWindowShouldClose(window))
	{
		glfwSwapBuffers(window);
		glfwPollEvents();
	}
	
	glfwTerminate();
	return 0;
}

  

void framebuffer_resize_callback(GLFWwindow* window, int width, int height)
{
	glViewport(0, 0, width, height);
}
```
A few ideas follow this code:
`glfwWindowHint` is useful for setting many options for the context window (such as width, height, autofocus, initialize minimized, etc). All options can be found in the [GLFW documentation](https://www.glfw.org/docs/latest/window.html#window_hints)

`glViewport` specifies the lower left corner (0, 0) and the upper right corner (800, 600) that will be used for the rendering window. OpenGL process coordinates from -1 to 1, the center of the screen being in (0, 0). Thus, the Viewport matches those coordinates to the specified rendering size (-1, -1)->(0, 0), (1, 1)->(800, 600). `framebuffer_resize_callback` is called whenever the user resizes the window (resize can be disabled with `glfwWinowHint`).

Inside the main loop, `glfwSwapBuffers` is called to swap between the *front* and *back* buffers. The *back* buffer is that we are drawing to inside the loop, and the *front* buffer contains the final output image that the user sees. This prevents flickering issues, because, without double buffers (like in immediate mode) the image is drawn pixel by pixel and "live" so the user may experience flickering.

`glfwPollEvents` checks if any events are triggered, updates the window state and calls the corresponding callback functions.


# Graphics Pipeline and Shaders
As in OpenGL everything is in 3D space, the process of transforming 3D coordinates to 2D pixels is managed by the graphics pipeline, which can be divided in two large parts:
The first transforms 3D coordinates into 2D coordinates and the second transforms those 2D coordinates into actual colored pixels.
Each step is highly specialized (have one specific function) and requires the output of the previous step as its input. The processing cores of the GPU run small programs for each step. These programs are called **shaders**.

Some of these shaders (such as vertex shader or fragment shader) are configurable by the developer. They run on the GPU and can save a lot of valuable CPU time. Shaders are written in OpenGL Shading Language (GLSL).
![[Pasted image 20240630193440.png]]
Each blue section represents where we can inject our own shaders.

## Vertex Data
As input to the graphics pipeline we pass in a list of three 3D coordinates that should form a triangle in an array called Vertex Data. This Vertex Data is a collection of vertices.

## Vertex
A vertex is a collection is a collection of data per 3D coordinate. This vertex's data is represented using ***vertex attributes*** that can contain any data we'd like.

## Primitives
In order for OpenGL to know what to do with the passed collection of coordinates and color, OpenGL requires to hint what kind of render type to form with the data. Those hints are called primitives and are given to OpenGL while calling drawing commands. Some primitives are: `GL_POINTS, GL_TRIANGLES, GL_LINE_STRIP`.

## Vertex Shader
Takes as input a single vertex and its main purpose is to transform 3D coordinates into different 3D coordinates and it allows us to do some basic processing on vertex attributes. The output is then (optionally) passed to the geometry shader.

## Geometry Shader
Takes as input a collection of vertices that form a primitive and has the ability to generate other shapes by emitting new vertices to form new/other primitives.

## Primitive Assembly
Takes as input all the vertices (or vertex if GL_POINTS is chosen) from the Vertex (or geometry) shader that form one or more primitives and assembles all the point(s) in the primitive shape given. The output is then passed to the rasterization stage.

## Rasterization Stage
Maps the resulting primitive(s) to the corresponding pixels on the final screen, resulting in fragments for the fragment shader.

***Clipping***:
Before the fragment shaders run, clipping is performed. Clipping discards all fragments that are outside your view.

## Fragment Shader
Calculate the final color of a pixel. Usually the fragment shader contains data about the 3D scene that it can use to calculate the final pixel color.

## Alpha test and Blending stage
Checks the corresponding depth (and stencil) value of the fragments and uses those to check if the resulting fragment is in front or behind other objects and should be discard accordingly. Also checks for alpha values (opacity) and blends the objects accordingly.

## Vertex Input
When passing vertex as input to the first process of the graphics pipeline (vertex shader), we need to create memory on the GPU where we store the vertex data, configure how OpenGL should interpret the memory and specify how to send the data to the graphics card.
### Vertex Buffer Objects (VBO)
VBOs are used to manage this memory, allowing to store a large number of vertices in the GPU's memory. The advantage of using VBOs is that we can send large batches of data all at once and keep it there (if there's enough memory left), without having to send data one vertex at a time.
As it is a type of OpenGL object (and there are more types of buffer objects), the type of a Vertex Buffer Object is represented by `GL_ARRAY_BUFFER`.

Simple code creating a VBO:
```cpp
// Triangle vertices
float vertices[] = {
	-0.5f, -0.5f, 0.0f,
	0.5f, -0.5f, 0.0f,
	0.0f, 0.5f, 0.0f
};

// Generate Vertex Buffer Object
unsigned int VBO = 0;
glGenBuffers(1, &VBO);

// Bind VBO spcecifying its type of Buffer
glBindBuffer(GL_ARRAY_BUFFER, VBO);

// Copy our vertices array to the currently bound buffer
/* ARGS:
* 1st: Type of the buffer (VBO is of type GL_ARRAY_BUFFER)
* 2nd: Size of the data in bytes
* 3rd: Data to be sent
* 4th: How the GPU should manage this data (GL_STREAM_DRAW, GL_STATIC_DRAW, GL_DYNAMIC_DRAW)
*/
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
```
In this code, we first generate a VBO and copy it's id to our VBO int. Then, we need to Bind it with `glBindBuffer`, changing the current `GL_ARRAY_BUFFER` bound in our state. Then, with `glBufferData` we copy our triangle vertices into the VBO in the GPU.
The 4th parameter specifies how we want the GPU to manage the given data:
- `GL_STREAM_DRAW`: the data is set only **once** and used by the GPU at most a few times.
- `GL_STATIC_DRAW`: the data is set only once and used many times.
- `GL_DYNAMIC_DRAW`: the data is changed a lot and used many times.


## GLSL and Shader creation and rendering
Basic Vertex Shader code:
```glsl
#version 330 core 
layout (location = 0) in vec3 aPos;
void main() 
{
	gl_Position = vec4(aPos.x, aPos.y, aPos.z, 1.0); 
}
```
GLSL is very similar to C. Every shader begins with a version declaration (3.3 core profile).
Next we declare all the input vertex attributes in the vertex shader with the `in` keyword and we specify its location (more on that later).
Since this is a simple code, we only set the pre-defined output variable `gl_Position` which is a vec4 (4th value is used for something called perspective division).

Basic Fragment Shader code:
```glsl
#version 330 core 
out vec4 FragColor; 
void main() 
{ 
	FragColor = vec4(1.0f, 0.5f, 0.2f, 1.0f); 
}
```
Fragment shader only requires one output variable that is a vec4 that defines the final color output that we calculate (4th value is alpha). Since it's an output, we use the `out` keyword.

Basic C++ code for shader object creation and compilation:
```cpp
// Create vertex shader object
unsigned int vertexShader = 0;
vertexShader = glCreateShader(GL_VERTEX_SHADER);
// attach source to vertex shader and compile it
glShaderSource(vertexShader, 1, &vertexShaderSource, nullptr);
glCompileShader(vertexShader);

// check for compile errors
int success = 0;
char infoLog[512];
glGetShaderiv(vertexShader, GL_COMPILE_STATUS, &success);
if (!success)
{
	glGetShaderInfoLog(vertexShader, 512, nullptr, infoLog);
	std::cout << "Error compiling vertex shader:\n" << infoLog << "\n";
}

// Create fragment shader object
unsigned int fragShader = 0;
fragShader = glCreateShader(GL_FRAGMENT_SHADER);
// attach source to fragment shader and compile it
glShaderSource(fragShader, 1, &fragmentShaderSource, nullptr);
glCompileShader(fragShader);

// check for compilation errors
glGetShaderiv(fragShader, GL_COMPILE_STATUS, &success);
if (!success)
{
	glGetShaderInfoLog(fragShader, 512, nullptr, infoLog);
	std::cout << "Error compiling fragment shader:\n" << infoLog << "\n";
}
```
The code is pretty much self-explanatory and the main difference between vertex and fragment shader compilation is the type of shader we pass into `glCreateShader`.

#### Shader Programs
A shader program object is the final linked version of multiple shaders combined. It is here that it links the outputs of each shader to the input of the next. 
The basic workflow is to create a shader program object, attach the shaders to it, link the program (check for errors) and then we activate it by using `glUseProgram` so that every shader and rendering call after it will now use this shader program.
Example of code:

### Vertex attributes
Vertex attributes allows us to specify how the GPU should process the vertex data and pass it as input to the vertex and fragment shaders. This allows us to specify any input we want.
As an example using our triangle vertices array:
```cpp
// Triangle vertices
float vertices[] = {
	-0.5f, -0.5f, 0.0f,
	0.5f, -0.5f, 0.0f,
	0.0f, 0.5f, 0.0f
};
```
![[Pasted image 20240701083329.png]]
- The position data is stored as 32-bit (4 byte) floating point values.
- Each position is composed of 3 of those values.
- There is no space (or other values) between each set of 3 values. They are *tightly packed*.
- The first value in the array is at the beginning of the buffer.

Now we specify how OpenGL should interpret the vertex data with vertex attributes, using `glVertexAttribPointer`:
```cpp
// specify vertex attributes for the data passed
/* ARGS:
* 1st: Location of which vertex attribute to configure (as in `layout (location=0)` in the vertex shader)
* 2nd: Size of the vertex attribute. Since it's a vec3, we use 3.
* 3rd: Type of the data.
* 4th: If the data should be normalized (only for integer,byte values)
* 5th: Stride. Specifies the space between consecutive vertex attributes.
* 6th: void* offset of where the vertex attrib begins.
*/
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);

// enable the vertex attrib (giving its location)
glEnableVertexAttribArray(0);
```
Since the data is tightly packed (no other values in between two consecutive vertex attributes) we could pass 0 as the stride and OpenGL would assume it based on the given size (3). But we can also use `3*sizeof(float)`.
The vertex attribute will operate on the data from memory managed by the currently bound VBO (`GL_ARRAY_BUFFER` bound with `glBindBuffer`).

### Vertex Array Object (VAO)
Since usually we handle a lot of object with different buffer objects and vertex attributes, configuring it for each of those objects every time we want to draw them can be a lot.
A vertex array object (VAO) can be bound just like a VBO and any subsequent vertex attribute calls from that point on will be stored inside the VAO. This has the advantage that when configuring vertex attribute pointers we only make those calls once, and whenever we want to draw the object, we can just bind the corresponding VAO.
So basically every object will consist in a VBO and a VAO, and when we want to draw it we just bind the corresponding VAO.
![[Pasted image 20240701090744.png]]
The process to generate a VAO is similar to that of a VBO:
```cpp
// Generate Vertex Array Object
unsigned int VAO = 0;
glGenVertexArrays(1, &VAO);
// bind the VAO
glBindVertexArray(VAO);
```

Then, a basic structure of a code to draw an object given its vertices is:
```cpp
// ..:: Initialization code (done once (unless your object frequently changes)) :: .. 
// 1. bind Vertex Array Object 
glBindVertexArray(VAO); 
// 2. copy our vertices array in a buffer for OpenGL to use 
glBindBuffer(GL_ARRAY_BUFFER, VBO); 
glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW); 
// 3. then set our vertex attributes pointers 
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0); glEnableVertexAttribArray(0); 

[...]

// ..:: Drawing code (in render loop) :: .. 
// 4. draw the object 
glUseProgram(shaderProgram); 
glBindVertexArray(VAO); 
/* ARGS:
*  1st: Primitive type to draw
*  2nd: Starting index of the vertex array
*  3rd: How many vertices
*/
glDrawArrays(GL_TRIANGLES, 0, 3).;
```
The `glDrawArrays` is an OpenGL function that draws primitives using the currently active shader, the previously defined vertex attribute configuration and with the VBO's vertex data (indirectly bound via the VAO).

### Element Buffer Objects
An Element Buffer Object (EBO) stores indices that OpenGL uses to decide the order of vertices to draw. It is useful when drawing object that require a lot of triangles and, instead of specifying every single vertex of every triangle (which would cause overlapping and repeating vertices), we specify the vertices of the object itself (like 4 vertices for a rectangle) and then we specify another array of indices that specify which vertices to draw (Indexed Drawing).

For example when drawing a rectangle we pass these vertices and indices:
```cpp
float rectVertices[] = {
	0.5f, 0.5f, 0.0f, // top right
	0.5f, -0.5f, 0.0f, // bottom right
	-0.5f, -0.5f, 0.0f, // bottom left
	-0.5f, 0.5f, 0.0f // top left
};

GLuint rectIndices[] = {
	0, 1, 3, // first triangle
	1, 2, 3 // second triangle
};
```

And then the process of generating and assigning data to VAO, VBO and also EBO is very similar:
```cpp
// Generate Vertex Array object for the rectangle and bind it
unsigned int rectVAO = 0;
glGenVertexArrays(1, &rectVAO);
glBindVertexArray(rectVAO);

// Generate VBO for the rectangle, copy data and bind it
unsigned int rectVBO = 0;
glGenBuffers(1, &rectVBO);
glBindBuffer(GL_ARRAY_BUFFER, rectVBO);
glBufferData(GL_ARRAY_BUFFER, sizeof(rectVertices), rectVertices, GL_STATIC_DRAW);

// Generate Element Buffer Object
unsigned int rectEBO = 0;
glGenBuffers(1, &rectEBO);
// bind ebo and copy the indices data to it
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, rectEBO);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(rectIndices), rectIndices, GL_STATIC_DRAW);

// specify vertex attributes for the rectangle data
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3*sizeof(float), (void*)0);
glEnableVertexAttribArray(0);
```

The only difference is that when we bind and pass data into our EBO, the type used is `GL_ELEMENT_ARRAY_BUFFER` and we pass in our indices array. The VAO also store calls to EBO bindings, so we only need to bind the VAO when drawing.

To draw, we also have to change the call from `glDrawArrays` to `glDrawElements`:
```cpp
// main loop
[...]

glUseProgram(shaderProgram);
glBindVertexArray(rectVAO);
// Draw rectangle using EBO
/* ARGS:
*  1st: Primitive mode to draw
*  2nd: Number of vertices to draw (based on number of indices)
*  3rd: Type of indices
*  4th: Offset or pass the indices, but we are using Element Buffer Object
*/
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);

[...]
```

![[Pasted image 20240701102913.png]]
## GLSL
Shaders are written in GLSL, a C-like language.
Shaders always begins with a version declaration, followed by a list of input and output variables, uniforms and its main function.

#### Structure
Typical structure of a shader:
```glsl
#version version_number (core,immediate)

in type input_var_name;
out type output_var_name;

uniform type uniform_name;

void main()
{
	// process input(s) and do some weird graphics stuff
	...
	// output processed stuff to output variable
	out_variable_name = weird_stuff_we_processed;
}
```

In the vertex shader, each input variable is also known as a vertex attribute. There is a maximum number of vertex attributes we're allowed to declare, that is limited by the hardware. This number can be retrieved through:
```cpp
int nrAttributes = 0;
glGetIntegerv(GL_MAX_VERTEX_ATTRIBS, &nrAttributes);
std::cout << "Maximum nr of vertex attrib supported: " << nrAttributes << "\n";
```
the minimum is usually 16.

#### Types
Basic types, such as: `int, float, double, uint, bool` and also vectors and matrices, such as:
- `vecn`: default vector of n floats
- `bvecn`: vector of n booleans
- `ivecn`: vector of n integers
- `uvecn`: vector of n unsigned integers
- `dvecn`: vector of n double components


#### Defaults `in` and `out` variables
Each shader can specify inputs and outputs using these keywords, and wherever an output variable matches with an input variable of the next shader they're passed along. When the types and the names are equal, OpenGL will link those variables together.

The vertex shader *must* receive some form of input straight from the vertex data, which we set in our C++ program. To define the inputs, we specify the input variables with location metadata (such as `layout (location=0)`).

The fragment shader requires a `vec4` color output variable.

Example of setting output from the vertex shader to input in the fragment shader:
Vertex Shader
```glsl
#version 330 core
layout (location = 0) in vec3 aPos; // position variable set at location 0 through the vertex attribute

out vec4 vertexColor; // specify color output to the fragment shader

void main()
{
	gl_Position = vec4(aPos, 1.0);
	vertexColor = vec4(0.5, 0.0, 0.0, 1.0); // set the output color to a dark-red
}
```

Fragment shader
```glsl
#version 330 core
out vec4 FragColor;

in vec4 vertexColor; // input variable from the vertex shader (same name and type)

void main()
{
	FragColor = vertexColor;
}
```

#### Uniforms
Uniforms are another way to pass data from our application on the CPU to the shaders on the GPU. Uniforms are global (a uniform variable is unique per shader program object, and can be accessed from any shader at any stage). Uniforms will keep their values until they're either reset or updated.

Declaration:
```glsl
#version 330 core
out vec4 FragColor;

uniform vec4 ourColor; // set this variable in the C++ code

void main()
{
	FragColor = ourColor;
}
```

To set the value for a uniform, we first get the index/location of the uniform attribute in our shader and then we can update its values:
```cpp
float timeVal = glfwGetTime();
float greenVal = (sin(timeVal) / 2.0f) + 0.5f;
int vertexColorLoc = glGetUniformLocation(shaderProgram, "ourColor");
glUseProgram(shaderProgram);
glUniform4f(vertexColorLoc, 0.0f, greenVal, 0.0f, 1.0f);
```
Finding the uniform location doesn't require to use the shader program first, but updating a uniform does require it.


#### Multiple vertex attributes in vertex data
We can pass in more than only positions in a VBO, as long as we use vertex attributes to tell OpenGL how to handle that data. 
For example, we can pass in colors in our triangle vertices array:
```cpp
float triVertices[] = {
	// positions        //colors
	-0.5f, -0.5f, 0.0f, 1.0f, 0.0f, 0.0f, // bottom right
	 0.5f, -0.5f, 0.0f, 0.0f, 1.0f, 0.0f, // bottom left
	 0.0f,  0.5f, 0.0f, 0.0f, 0.0f, 1.0f // top
};

[...]

// position vertex attrib
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 6*sizeof(float), (void*)0);
glEnableVertexAttribArray(0);
// color vertex attrib
glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 6*sizeof(float), (void*)(3*sizeof(float)));
glEnableVertexAttribArray(1);
```
Since now we have two vertex attributes in our vertex data, the size of the stride is not `3*sizeof(float)` anymore, since the separation between two separate vertex attributes is now 6 floats.
Also, for the color vertex attribute, we have to set an offset of 3 float values, because the first 3 values in our data are position values. And it's location is 1, since vertex attrib at location 0 is the position.

Then we have to change our input and output variables in the vertex shader and in the fragment shader:
Vertex Shader
```glsl
#version 330 core
layout (location = 0) in vec3 aPos; // vertex attrib at location 0
layout (location = 1) in vec3 aColor; // vertex attrib at location 1

out vec3 ourColor; // output a color to the frag shader

void main()
{
	gl_Position = vec4(aPos, 1.0);
	ourColor = aColor; // set output variable to the color we get from the input shader
}
```
Fragment Shader
```glsl
#version 330 core
out vec4 FragColor;
in vec3 ourColor; // same name and type from vertex shader

void main()
{
	FragColor = vec4(ourColor, 1.0);
}
```
***Fragment Interpolation***:
The resulting triangle is:
![[Pasted image 20240702083936.png]]
Since the rasterization stage usually results in a lot more fragment than vertices originally specified, it interpolates all the fragment shader's input variables.


# Using Textures
A texture is a 2D image (1D or 3D too) that adds detail to an object. Textures can also be used to store a large collection of arbitrary data to send to the data (height map, etc).

## Texture Sampling
In order to map a texture to the triangle, we need to specify for every vertex of the triangle which part of the texture it corresponds to. Each vertex thus should have a **texture coordinate** associated with it. 

**Texture coordinates** range from 0 to 1 in the x and y axis (for 2D texture images). Retrieving the texture color using texture coordinates is called *sampling*. (0,0) is bottom left and (1,1) is upper right.

Example:
![[Pasted image 20240702102628.png]]
As we want to match the bottom left triangle with the bottom left of the texture, and same for the other 2 vertices, these are the resulting texture coordinates:
```cpp
float texCoords[] = {
	0.0f, 0.0f, // lower-left corner
	1.0f, 0.0f, // lower-right corner
	0.5f, 1.0f  // top-center corner
};
```

## Texture Wrapping
If we specify coordinates outside of the range of the texture, that is (0, 0) to (1, 1), OpenGL will wrap the texture and, by default, will repeat the texture images.
There are 4 options for texture wrapping:
- `GL_REPEAT`: Default behavior. Repeats the texture image.
- `GL_MIRRORED_REPEAT`: Mirrors the image with each repeat.
- `GL_CLAMP_TO_EDGE`: Clamps the coordinates between 0 and 1. Higher coordinates become clamped to the edge, resulting in a stretched edge pattern.
- `GL_CLAMP_TO_BORDER`: Coordinates outside the range are now given a user-specified  border color
Resulting examples (order is the same as above):
![[Pasted image 20240702103153.png]] 
Each of these options can be set per coordinates axis (s,t,r equivalent to x,y,z) with the `glTexParameter*` function:
```cpp
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_MIRRORED_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
```
- 1st argument: specifies the texture target (2D textures in this case).
- 2nd argument: what option to set and for which texture axis.
- 3rd argument: which option to set. In this case (texture wrap), we specify which wrapping method to use.

## Texture Filtering
Texture coordinates do not depend on resolution and thus can be any floating point value. OpenGL has to figure out which texture pixel (*texel*) to map the texture coordinate to.
There are several options for texture filtering, but the most important are `GL_NEAREST` and `GL_LINEAR`.
- `GL_NEAREST` is the default method for texture filtering. OpenGL selects the texel that its center is closest to the texture coordinate specified.
- `GL_LINEAR` takes an interpolated value from the texture's coordinate's neighboring texels, approximating a color between the texels. The smaller the distance from the texture coordinate to a texel's center, the more that texel's color contributes to the sampled color.
![[Pasted image 20240702104438.png]]
Texture filtering can be set for magnifying (scaling up) and minifying (scaling down) operations using the same function `glTexParameteri`:
```cpp
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_NEAREST); glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```

## Mipmaps
Objects far away with the same high resolution texture attached as objects that are closer to the viewer produce probably only a few fragments, so OpenGL has difficulties retrieving the right color value.

To solve this issue, OpenGL uses mipmaps, that basically are a collection of textures images where each subsequent texture is twice as small compared to the previous one (such as 64x64, then 32x32, then 16x16...).
After a certain distance from the object, OpenGL will use a different mipmap texture that best suits that distance.

Example of a mipmapped texture:
![[Pasted image 20240702105027.png]]

OpenGL is able to do all the work of generating mipmaps with a single call to `glGenerateMipmap` after creating the texture. It is also possible to filter between mipmap levels using NEAREST and LINEAR filtering for switching between mipmap levels:
- `GL_NEAREST_MIPMAP_NEAREST`: takes the nearest mipmap to match the pixel size and uses nearest neighbor interpolation for texture sampling.
- `GL_LINEAR_MIPMAP_NEAREST`: takes the nearest mipmap level and samples that level using linear interpolation.
- `GL_NEAREST_MIPMAP_LINEAR`: linearly interpolates between the two mipmaps that most closely match the size of a pixel and samples the interpolated level via nearest neighbor interpolation.
- `GL_LINEAR_MIPMAP_LINEAR`: linearly interpolates between the two closest mipmaps and samples the interpolated level via linear interpolation.

We can set the filtering method using `glTexParameteri` as well:
```cpp
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glTextParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
```

***TEXTURE MAGNIFICATION DOESN'T USE MIPMAPS***. Setting one of the mipmap filtering options as the magnification filter is a mistake, since mipmaps are primarily used for downscaling textures.


## Loading and Creating Textures
Loading textures can be a hell of a job because of the many formats a texture file can be.
[stb_image.h](https://github.com/nothings/stb/blob/master/stb_image.h) is a single header image loading library that is able to load most popular formats. It is easy to use since it's a single header file, so it just needs to be included and define a preprocessor directive `STB_IMAGE_IMPLEMENTATION`.

This is a simple code using stb to load the image and then generating a texture through OpenGL:
```cpp
// generating OpenGL texture
unsigned int texture{};
glGenTextures(1, &texture);

// bind texture (from here on any subsequent texture commands will configure the currently bound texture)
glBindTexture(GL_TEXTURE_2D, texture);

// set texture wrapping/filtering options (on the currently bound texture)
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);

// load image data
int width, height, nrChannels;
unsigned char* data = stbi_load("textures/container.jpg", &width, &height, &nrChannels, 0);

// load data into texture
/* ARGS:
* 1st: Texture target (2D texture in this case)
* 2nd: Mipmap level, if settings mipmap level manually
* 3rd: Format to store the image. (RGB values in this case)
* 4th: width of resulting texture
* 5th: height of resulting texture
* 6th: always 0 (legacy stuff)
* 7th: format of source image
* 8th: datatype of the source image
* 9th: loaded image data
*/
glTexImage2D(GL_TEXTURE_2D, 0, GL_RGB, width, height, 0, GL_RGB, GL_UNSIGNED_BYTE, data);

// generate mipmaps (currently bound texture)
glGenerateMipmap(GL_TEXTURE_2D);

// free image memory
stbi_image_free(data);
```

## Applying textures
The basic workflow for applying textures, after generating them as before, is to specify the texture coordinates in our vertex data, assign a vertex attribute to it, then in our fragment shader we'll use the `texture()` function to apply it to the output `FragColor`. And then when drawing we need to bind the texture before so that OpenGL passes our texture directly into the fragment shader.
Example:
C++ code
```cpp
// using the same rectangle verticies as before, but with color and tex coordinates now
float rectVertices[] = {
	 // positions        // colors          // texture coords
	 0.5f,  0.5f, 0.0f,  1.0f, 0.0f, 0.0f,  1.0f, 1.0f, // top right
	 0.5f, -0.5f, 0.0f,  0.0f, 1.0f, 0.0f,  1.0f, 0.0f, // bottom right
	-0.5f, -0.5f, 0.0f,  0.0f, 0.0f, 1.0f,  0.0f, 0.0f, // bottom left
	-0.5f,  0.5f, 0.0f,  0.0f, 1.0f, 1.0f,  0.0f, 1.0f  // top left
};
GLuint rectIndices[] = {
	0, 1, 3, // first triangle
	1, 2, 3 // second triangle
};

[...]

// position vertex attribute (location 0)
glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 8*sizeof(float), (void*)0);
glEnableVertexAttribArray(0);

// color vertex attribute (location 1)
glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 8*sizeof(float), (void*)(3*sizeof(float)));
glEnableVertexAttribArray(1);

// texture coord vertex attribute (location 2)
glVertexAttribPointer(2, 2, GL_FLOAT, GL_FALSE, 8*sizeof(float), (void*)(6*sizeof(float)));
glEnableVertexAttribArray(2);

[...]

// -- inside main loop ---
// Draw the rectangle using EBO
glBindTexture(GL_TEXTURE_2D, texture);
glBindVertexArray(rectVAO);
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
```

Vertex Shader
```glsl
#version 330 core

layout (location = 0) in vec3 aPos;
layout (location = 1) in vec3 aColor;
layout (location = 2) in vec2 aTexCoord;

out vec3 ourColor;
out vec2 TexCoord;

void main()
{
    gl_Position = vec4(aPos, 1.0);
    ourColor = aColor;
    TexCoord = aTexCoord;
}
```

Fragment Shader
```glsl
#version 330 core

out vec4 FragColor;

in vec3 ourColor;
in vec2 TexCoord;

uniform sampler2D ourTexture; // sampler is a data-type for texture obejcts

void main()
{
    FragColor = texture(ourTexture, TexCoord);
}
```
When binding the texture before drawing, OpenGL will automatically set the value for the uniform sampler2D variable `ourTexture`.

## Texture Units
A texture unit represents simply a location of a texture. In the previous fragment shader, we use a uniform variable but we don't assign anything to it. That's because by default the unit for a texture is 0, which is the default active texture unit, so a `uniform sampler2D` is set to 0 by default, using the 0 texture unit.

Texture units allows us to use more than 1 texture in our shaders. Without it there's no way to bind more than 1 texture at a time. So we can bind multiple textures as long as we active the corresponding unit first.
For example:
```cpp
glActiveTexture(GL_TEXTURE0); // activate texture unit 0
glBindTexture(GL_TEXTURE_2D, texture); // bind texture to the currently active unit
```

OpenGL should have at least a minimum of 16 texture units (`GL_TEXTURE0` to `GL_TEXTURE15`). They are defined in order, so for example `GL_TEXTURE8 = GL_TEXTURE0 + 8`, which is useful for loops.

The fragment shader must accept another sampler:
```glsl
#version 330 core
[...]
uniform sampler2D texture1; // we will set this to be GL_TEXTURE0 in the C++ code
uniform sampler2D texture2; // we will set this to be GL_TEXTUREWHATEVER in the C++ code 

void main()
{
	FragColor = mix(texture(texture1, TexCoord), texture(texture2, TexCoord), 0.2);/
}
```
in the above example we mix two textures together with an interpolation rate (third argument), which we specified 0.2, so it'll be 80% of the first texture and 20% of the second.

# Transformations
## Scaling
Scaling a vector means increasing the length of the arrow by the amount we'd like to scale.
For example, scaling the vector $\vec{v} = (3, 2, 0)$ by 0.5 in the x-axis and 2 in the y-axis (a *non-uniform* scale, since the scaling factor is not the same) (also considering scale z by 1) we would have $\vec{v}_1 = (1.5, 4, 0)$.
This means that to create a matrix for scaling is to simply change the 1's in the identity matrix 4x4 by each scaling factor.
So, if we represent the scaling factors as a vector, $(S_1, S_2, S_3)$, and our vector as $(x, y, z)$, we have:
$$
\left[ \begin{array} _S_1 & 0 & 0 & 0 \\ 0 & S_2 & 0 & 0 \\ 0 & 0 & S_3 & 0 \\ 0 & 0 & 0 & 1 \end{array} \right] \cdot \left( \begin{array} _x \\ y \\ z \\ 1 \end{array} \right) = \left( \begin{array} _S_1 \cdot x \\ S_2 \cdot y \\ S_3 \cdot z \\ 1 \end{array} \right)
$$
The fourth component ($w = 1$) will be kept as 1 and will be explained later.

## Translation
Translation is the process of moving the vector based on a translating vector, by adding this vector on top of the original to return a new one with a different position.
Representing the translation vector as $(T_x, T_y, T_z)$, we have:
$$
\left[ \begin{array} _1 & 0 & 0 & T_x \\ 0 & 1 & 0 & T_y \\ 0 & 0 & 1 & T_z \\ 0 & 0 & 0 & 1 \end{array} \right] \cdot \left( \begin{array} _x \\ y \\ z \\ 1 \end{array} \right) = \left( \begin{array} _x + T_x \\ y + T_y \\ z + T_z \\ 1 \end{array} \right)
$$

### Homogeneous coordinates ($w$ component)
The $w$ component of a vector is also known as a homogeneous coordinate. Using it has several advantages, one of them is allowing us to do matrix translations on 3D vectors (without a $w$ component we can't translate vectors). Also, it is used to create 3D perspective.

If the homogeneous coordinate is equal to 0, then the vector is specifically known as a direction vector (since it can't be translated).

## Rotation
A rotation in 2D or 3D is represented with an angle (preferably in radians). Rotations in 3D are specified with an angle *and* a **rotation axis**, so the angle rotates the object along the rotation axis.
A rotation matrix is defined for each unit axis in 3D space:
- Rotation around X-axis:
$$
\left[ \begin{array} _1 & 0 & 0 & 0 \\ 0 & \cos{\theta} & -\sin{\theta} & 0\\ 0 & \sin{\theta} & \cos{\theta} & 0 \\ 0 & 0 & 0 & 1 \end{array} \right] \cdot \left( \begin{array} _x \\ y \\ z \\ 1 \end{array} \right) = \left( \begin{array} _x \\ \cos{\theta} \cdot y - \sin{\theta} \cdot z \\ \sin{\theta} \cdot y + \cos{\theta} \cdot z \\ 1 \end{array} \right)
$$
- Rotation around Y-axis:
$$
\left[ \begin{array} _\cos{\theta} & 0 & \sin{\theta} & 0 \\ 0 & 1 & 0 & 0 \\ -\sin{\theta} & 0 & \cos{\theta} & 0 \\ 0 & 0 & 0 & 1 \end{array} \right] \cdot \left( \begin{array} _x \\ y \\ z \\ 1 \end{array} \right) = \left( \begin{array} _\cos{\theta} \cdot x + \sin{\theta} \cdot z \\ y \\ -\sin{\theta} \cdot x + \cos{\theta} \cdot z \\ 1 \end{array} \right)
$$
- Rotation around Z-axis:
$$
\left[ \begin{array} _\cos{\theta} & -\sin{\theta} & 0 & 0 \\ \sin{\theta} & \cos{\theta} & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{array} \right] \cdot \left( \begin{array} _x \\ y \\ z \\ 1 \end{array} \right) = \left( \begin{array} _\cos{\theta} \cdot x - \sin{\theta} \cdot y \\ \sin{\theta} \cdot x + \cos{\theta} \cdot y \\ z \\ 1 \end{array} \right)
$$

Rotating around the 3 axis by combining those rotations first around the X-axis, then Y and then Z introduces a problem of [Gimbal Lock](https://en.wikipedia.org/wiki/Gimbal_lock). 
The other is to rotate around an arbitrary unit axis (e.g. $(0.662, 0.2, 0.722)$). This matrix gets fucking big, with $(R_x, R_y, R_z)$ as the arbitrary rotation axis:
$$
\begin{bmatrix}
\cos \theta + R_x^2 (1 - \cos \theta) & R_x R_y (1 - \cos \theta) - R_z \sin \theta & R_x R_z (1 - \cos \theta) + R_y \sin \theta & 0 \\
R_y R_x (1 - \cos \theta) + R_z \sin \theta & \cos \theta + R_y^2 (1 - \cos \theta) & R_y R_z (1 - \cos \theta) - R_x \sin \theta & 0 \\
R_z R_x (1 - \cos \theta) - R_y \sin \theta & R_z R_y (1 - \cos \theta) + R_x \sin \theta & \cos \theta + R_z^2 (1 - \cos \theta) & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
This matrix doesn't completely prevent Gimbal Lock, but does make it harder. To truly prevent it, it is best to use [Quaternions](https://www.youtube.com/watch?v=zjMuIxRvygQ), which will not be covered in this course. 

## Combining matrices
We can combine multiple transformations in a single matrix thanks to matrix-matrix multiplication.
Matrix multiplication is not commutative, so *their order is important*. Every multiplication should be right to left, because the right-most matrix is first multiplied with the vector. 
The advised order is to first do scaling operations, then rotations and lastly translations:
$$
Transform = Trans \cdot Rotation \cdot Scale
$$
## GLM
[GLM](https://github.com/g-truc/glm) stands for OpenGL Mathematics and is a header-only library that allows us to do a lot of math operations easily.
Most of GLM's functionality that we need can be found in 3 headers files:
```cpp
#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>
```

As an example, using it to translate a vector $(1, 0, 0)$ by $(1, 1, 0)$:
```cpp
glm::vec4 vec(1.0f, 0.0f, 0.0f, 1.0f); // initialize vec as (1, 0, 0) with w=1 as well
glm::mat4 trans = glm::mat4(1.0f); // create 4x4 identity matrix 
trans = glm::translate(trans, glm::vec3(1.0f, 1.0f, 0.0f)); // create transformation matrix
vec = trans * vec; // get our resulting translated vector
```
Note that the transformation matrix is created by calling `glm::translate` with a translation vector ($1, 1, 0$) which essentially just multiply the given matrix (`trans`) with a translation matrix of that translation vector.

Example of scaling and rotating:
```cpp
glm::mat4 trans = glm::mat4(1.0f); // initialize 4x4 identity matrix
trans = glm::rotate(trans, glm::radians(90.0f), glm::vec3(0.0, 0.0, 1.0)); // rotate 90° along the z-axis
trans = glm::scale(trans, glm::vec3(0.5, 0.5, 0.5)); // scale by a factor of (0.5, 0.5, 0.5)
```
Note that matrix operations are done from right to left. So in this case, besides scaling last, the resulting transform matrix would look like:
$$
Transform = Rotate(90°, (0,0,1)) \cdot Scale(0.5, 0.5, 0.5)
$$
It is important that the axis we rotate around should be a unit vector.

To pass the transformation matrix into our shaders, we can use GLSL's built in `mat4` type and pass it as a uniform variable in the vertex shader:
```glsl
#version 330 core
layout (location = 0) in vec3 aPos;
layout (location = 1) in vec2 aTexCoord;

out vec2 TexCoord;
  
uniform mat4 transform;

void main()
{
    gl_Position = transform * vec4(aPos, 1.0f);
    TexCoord = vec2(aTexCoord.x, aTexCoord.y);
} 
```
To change that uniform we use `glUniformMatrix4fv` in our C++ code and pass in our `trans` matrix using `glm::value_ptr(trans)`, because it needs to be passed as a pointer.

# Coordinate Systems
OpenGL expects all the vertices (that we want to be visible) to be in normalized device coordinates (NDC) after each vertex shader run. That is, for x, y, and z coordinates of each vertex to be between -1 and 1.
A better workflow is to specify the coordinates in a range (or space) and in the vertex shader we transform these coordinates to (NDC). These NDC are then given to the rasterizer to transform them to 2D coordinates/pixels/fragments on your screen.

Transforming coordinates to NDC is usually accomplished in a step-by-step where we transform an object's vertices to several intermediate coordinate systems before finally transforming them to NDC. The advantage of using these intermediate coordinate systems is that some operations/calculations are easier in certain of them.
There are a total of 5 different coordinate systems that are important to us:
- Local space (or Object space)
- World space
- View space (or Eye space)
- Clip space
- Screen space

To transform the coordinates systems from one to the next, we use several transformation matrices of which the most important are the *model*, *view* and *projection* matrix.
Our vertex coordinates first start in local space as *local coordinates*, then are further processed to *world coordinates*, *view coordinates*, *clip coordinates* and finally *screen coordinates*.
![[Pasted image 20240703104341.png]]
- Local coordinates: Coordinates of your object relative to its local origin.
- World-space coordinates: Coordinates in respect of a larger world, relative to some global origin.
- View-space coordinates: Coordinates as seen from the camera/viewer's point of view.
- Clip coordinates: Coordinates processed to the -1.0 and 1.0 range and determine which vertices end up on the screen.
- Screen coordinates: Coordinate range defined by `glViewport`. We get this in a process called *viewport transform*. The resulting coordinates are then sent to the rasterizer to turn them into fragment.

## Local-Space to World-Space and Model Matrix
The transformation from local to world space is accomplished with this model matrix. This is a transformation that translates, scales and/or rotates your object to place it in the world at a location/orientation they belong to.

## View Space and View Matrix
It is usually referred as the camera of OpenGL (also known as camera space or eye space). It is the result of transforming your world-space coordinates to coordinates that are in front of the user's view. It is the space as seen from the camera's point of view. The combinations of transformations to accomplish this transition are stored inside a *view matrix* that transform world space to view space.

## Clip Space
At the end of each vertex shader run, OpenGL expects the coordinates to be within a specific range (-1.0 and 1.0) and any coordinates that falls outside of this range is *clipped*. 

To transform vertex coordinates from view to clip-space we define a ***projection matrix*** that specifies a range of coordinates (e.g. -1000 to 1000) for each axis, then it converts coordinates within this range to NDC (-1.0 to 1.0) (not directly, there is a step called Perspective Division in between). All coordinates outside this range will not be mapped and therefore will be clipped.
If only a part of a primitive is outside the clipping volume, OpenGL will reconstruct the primitive as one or more primitives to fit inside the clipping range.

### Projection and frustum
The viewing box a projection matrix creates is called a *frustum*, and each coordinate that ends up inside this frustum will end up in the user's screen.
Projection is the total process of converting coordinates within a specified range to NDC. The projection matrix projects 3D coordinates to the easy-to-map-to-2D NDC.

Once all vertices are transformed to clip space, a final operation called perspective division is performed where we divide the x, y and z components of the position vectors by the vector's homogeneous w component.

There's two types of projection: *orthographic* projection and *perspective* projection.
### Orthographic projection
An orthographic projection defines a cube-like frustum box that defines the clipping space where each vertex outside this box is clipped. When creating an orthographic projection matrix we specify the width, height and length of the visible frustum.
![[Pasted image 20240703110817.png]]
Any coordinate in front of the near plane is clipped and the same applies to coordinates behind the far plane. The orthographic frustum directly maps all coordinates inside the frustum to NDC without any side effects since it won't touch the w component of the transformed vector.

To create an orthographic projection matrix we make use of GLM's function `glm::ortho`:
```cpp
/* ARGS:
*  1st: left part/coordinate of the frustum
*  2nd: right part/coordinate of the frustum
*  3rd: bottom part/coordinate of the frustum
*  4th: top part/coordinate of the frustum
*  5th: distance from the near plane
*  6th: distance between near and far plane
*/
glm::ortho(0.0f, 800.0f, 0.0f, 600.0f, 0.1f, 100.0f);
```
The 1st and 2nd argument specifies the width of the near and far planes, the 3rd and 4th specifies the height of the planes.

Orthographic projection produces unrealistic results since the projection doesn't take perspective into account.
### Perspective projection
Perspective is what in real life creates that effect where further away objects appear smaller:
![[Pasted image 20240703111609.png]]
Due to perspective, the lines seem to coincide at a far enough distance. This is the effect that perspective projection tries to mimic, and it does so using a *perspective projection matrix*.

The projection matrix maps a given frustum range to clip space, but also manipulates the w value of each vertex coordinate in such a way that the further away a vertex coordinate is from the viewer, the higher this w component becomes. Once the coordinates are transformed to clip space they fall in the range from -w to w. Since OpenGL requires visible coordinates to fall between -1.0 and 1.0, perspective division is applied to the clip space coordinates:
$$
out = \left( \begin{array} _x/w \\ y/w \\ z/w \end{array} \right)
$$

GLM also has a function to crete a perspective projection matrix:
```cpp
/* ARGS:
*  1st: FOV (how large the viewspace is)
*  2nd: Aspect ratio (ratio between width and height of the viewport)
*  3rd: distance to near plane
*  4th: distance from near to far plane
*/
glm::mat4 proj = glm::perspective(glm::radians(45.0f), (float)width/(float)height), 0.1f, 100.0f);
```

The resulting frustum is like a pyramid:
![[Pasted image 20240703113016.png]]

Comparison between orthographic and perspective projections:
![[Pasted image 20240703113235.png]]


## Combining everything
A vertex coordinate is transformed to clip coordinates as follows:
$$
V_{clip} = M_{projection} \cdot M_{view} \cdot M_{model} \cdot V_{local}
$$
(the order is important)

## Going 3D

### Model matrix setup
To start drawing 3D we first create a model matrix. The model matrix consists of translations, scaling and/or rotations we'd like to apply to transform all object's vertices to the global world space.

In this example, we simply rotate it on the x-axis (our rectangle will then look like a plane laying on the floor, and it will represent the plane in the global world):
```cpp
glm::mat4 model = glm::mat4(1.0f);
model = glm::rotate(model, glm::radians(-55.0f), glm::vec3(1.0f, 0.0f, 0.0f));
```

Every unique transformation that we do to an object will be composed in the model matrix as well (every object has their single model matrix, that can be transformed after a global model matrix or not).

### View matrix setup
Next is the view matrix (to get our camera view). Notice that if we move our camera slightly backwards, it is the same as moving the entire scene slightly forward. 
The view matrix essentially does this, it moves the entire scene around inverted to where we want the camera to move.

For that, it is important to know that OpenGL +y-axis is upwards in the screen, +x-axis is to the right in the screen and +z-axis is directed outside the screen:
![[Pasted image 20240703114715.png]]

For now our camera is static, so the view matrix (for example) looks like this:
```cpp
// View matrix (static camera, only move backwards a bit, so the entire world moves forward)
glm::mat4 view = glm::mat4(1.0f);
view = glm::translate(view, glm::vec3(0.0f, 0.0f, -3.0f));
```

### Projection matrix setup
In this case we will use perspective projection with 45° fov:
```cpp
// Projection matrix (in this case perspective)
glm::mat4 projection = glm::perspective(glm::radians(45.0f), (float)WINDOW_WIDTH / (float)WINDOW_HEIGHT, 0.1f, 100.0f);
```

Lastly, we just pass every matrix into our vertex shader as uniforms:
```glsl
#version 330 core 
layout (location = 0) in vec3 aPos; 
... 
uniform mat4 model; 
uniform mat4 view; 
uniform mat4 projection; 

void main() 
{
	// note that we read the multiplication from right to left 
	gl_Position = projection * view * model * vec4(aPos, 1.0); 
	... 
}
```
and in our C++ we just need to update the uniforms (preferably every frame, since transformations matrices tend to change a lot).

### Z-Buffer and Depth test
When drawing a 3D object, like a cube, OpenGL may overwrite any pixel color that may have already been drawn there before, so some triangles may appear on top of each other.

The z-buffer, or depth buffer, stores the depth of each vertex within each fragment (as the fragment's z value) and whenever the fragment wants to output its color, OpenGL compares its depth values with the z-buffer. This process is called *depth testing* and is done automatically by OpenGL.

To use it we first need to enable it using `glEnable`, and we need to also clear the depth buffer at every frame (just like the color buffer):
```cpp
glEnable(GL_DEPTH_TEST);
[...]

// inside render loop
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
```

# Camera and Movement
Camera is not an intrinsic concept of OpenGL, but we can simulate one to be our point of view by manipulating the view matrix and moving the entire scene in the reverse direction.

Camera/view space is the space where all the vertex coordinates are as seen from the camera's perspective as the origin of the scene: the view matrix transforms all the world coordinates into view coordinates that are relative to the *camera's position and direction*.
To define a camera we need its position in world space, the direction it's looking at, a vector pointing to the right and a vector pointing upwards from the camera.
![[Pasted image 20240704083935.png]]

1. Camera Position: we just need to define a vector in world space that points to the camera's position, such as:
```cpp
glm::vec3 cameraPos = glm::vec3(0.0f, 0.0f, 3.0f);
```

2. Camera Direction: This is the direction to which the camera points, so we need to have a `cameraTarget`, and the direction will be the unit vector of the subtraction between `cameraTarget` and `cameraPosition`. Since we're moving the entire scene reverse from where we want to go, the direction will be inverted as well:
```cpp
glm::vec3 cameraTarget = glm::vec3(0.0f, 0.0f, 0.0f);
glm::vec3 cameraDirection = glm::normalize(cameraPos - cameraTarget);
```

3. Camera Right axis: To get the right vector, we first specify an up vector that points upwards (in world space) and then do a cross product between that and the `cameraDirection`, since the result will be a perpendicular vector:
```cpp
glm::vec3 up = glm::vec3(0.0f, 1.0f, 0.0f);
glm::vec3 cameraRight = glm::normalize(glm::cross(up, cameraDirection));
```

4. Camera Up axis: now we just need a cross product between the camera's direction and the camera's right axis:
```cpp
glm::vec3 cameraUp = glm::cross(cameraDirection, cameraRight);
```

## Look At
The *LookAt* matrix is essentially a matrix with those 3 perpendicular axes plus a translation vector and we're able to transform any vector to that coordinate space by multiplying it with this matrix:
$$
LookAt = \left[ \begin{array} _R_x & R_y & R_z & 0 \\ U_x & U_y & U_z & 0 \\ D_x & D_y & D_z & 0 \\ 0 & 0 & 0 & 1 \end{array} \right] * \left[ \begin{array} _1 & 0 & 0 & -P_x \\ 0 & 1 & 0 & -P_y \\ 0 & 0 & 1 & -P_z \\ 0 & 0 & 0 & 1 \end{array} \right]
$$
Where $R$ is the right vector, $U$ is the up vector, $D$ is the direction vector, and $P$ is the camera's position vector.

Using this LookAt matrix as our view matrix effectively transform all the world coordinates to the view space we just defined. It creates a view matrix that *looks at* a given target.

GLM has a function to calculate the LookAt matrix, we only need to specify the camera's position, a target position and a vector that represents the up vector in world space:
```cpp
glm::mat4 view;
view = glm::lookAt(cameraPosition, cameraTarget, worldUp);
```

## DeltaTime
To calculate the `deltaTime` (time elapsed between two consecutive frames) we keep track of 2 variables:
```cpp
float deltaTime = 0.0f;
float lastFrame = 0.0f;
```
and within each frame we calculate them:
```cpp
float currentFrame = glfwGetTime();
deltaTime = currentFrame - lastFrame;
lastFrame = currentFrame;
```


# Lighting
## Colors
The color we observe of an object is not the color it actually has, but the color it reflects from the source. The colors that are not absorbed by the object is the color we perceive of it.

In computer graphics, we define a light source in OpenGL and the color of this light source.
If we multiply the light source's color with an object's color value, the resulting color would be the reflected color of the object (and thus its perceived color).
For example, using a coral colored (`(R=1.0,G=0.5,B=0.31)`) object:
```cpp
glm::vec3 lightColor(1.0f, 1.0f, 1.0f); // White light
glm::vec3 toyColor(1.0f, 0.5f, 0.31f);
glm::vec3 result = lightColor * toyColor; // = (1.0f, 0.5f, 0.31f) 
```

This way, we can **define an object's color** as *the amount of each color component it reflects from a light source*. In this case, the `toyColor` reflects 100% (`1.0f`) of red light, and thus the result is 100% of that red light; 50% of green light, so the result is 50% of the green light source, and 31% of blue light.

## Lighting Scene
Since we'll be using light sources, we want to display them as visual objects in the scene and add at least one object to simulate the lighting from.

Using the same mesh as the cube (same vertices), we can draw the light source as a cube and with it's light color. The only different thing needed will be a different VAO for the light source, and a different shader.

The normal lighting shader, that will be used by other objects that are not light sources will take two uniforms: `objectColor` and `lightColor`:
```glsl
#version 330 core

uniform vec3 objectColor;
uniform vec3 lightColor;

void main()
{
	gl_FragColor = vec4(lightColor * objectColor, 1.0);
}
```

Since we don't want our light source to be affected, we use a different shader to draw the light source so it maintains a constant bright color, such as:
```glsl
#version 330 core

uniform vec3 lightColor;

void main()
{
	gl_FragColor = vec4(lightColor, 1.0);
}
```

And then we just set a `glm::vec3` position for the light source and render it's object in our scene to indicate where the light comes from.

# Basic Lighting
Lighting in the real world is way more complicated and depends on way too many factors. Lighting in OpenGL is therefore based on approximations of reality using simplified models that are much easier to process and look relatively similar.
These lighting models are based on the physics of light as we understand it.

## Phong Lighting model
Phong lighting is a model based on the physics of light. The major building blocks of this model consists of 3 main components: *ambient*, *diffuse* and *specular* lighting.
- **Ambient lighting**: even when it is dark there is usually still some light somewhere in the world (the moon, a distant light, etc) so objects are almost never completely dark. To simulate this we use an ambient lighting constant that always gives the object some color.
- **Diffuse lighting**: simulates the direction impact a light object has on an object. The more a part of an object faces the light source, the brighter it becomes.
- **Specular lighting**: simulates the bright spot of a light that appears on shiny objects. Specular highlights are more inclined to the color of the light than the color of the object.
![[Pasted image 20240708112828.png]]

## Ambient lighting
One of the properties of light is that it can scatter and bounce in many directions, reaching spots that aren't directly visible, light can thus reflect on other surfaces and have an indirect impact on the lighting of an object. Algorithms that take this into consideration are called global illumination algorithms, but there are too complicated and expensive to calculate.

A very simplistic model of global illumination is *ambient lighting*. We use a small constant (light) color that we add to the final resulting color of the object's fragments.
We just take the light's color, multiply it with a small constant ambient factor, multiply this with the object's color and use that as the fragment's color in the cube object's shader:
```glsl
[...]
void main()
{
	float ambientStrength = 0.1;
	vec3 ambient = ambientStrength * lightColor;

	vec3 result = ambient * objectColor;
	gl_FragColor = vec4(result, 1.0);
}
```

## Diffuse lighting
Diffuse lighting gives the object more brightness the closer it's fragments are aligned to the light rays from a light source.
![[Pasted image 20240708113658.png]]
We need to measure at what angle the light ray touches the fragment. If the light ray is parallel with the surface's normal vector (and thus perpendicular to the surface) then the light has the greatest impact. 

The angle can be easily calculated with dot product. Since we need to get the cosine of the angle using the dot product, we need to make sure that *all vectors are normalized*.

The directed light ray will be the difference between the light's position and the fragment's position.

### Normal vectors
A normal vector is a unit vector that is perpendicular to the surface of a vertex. Since a vertex by itself has no surface we retrieve a normal vector by using its surrounding vertices, using a little trick by using the cross product to get the normal vector. But on not complicated shapes (like a cube) we can simply manually add them to the vertex data.

So in the code we just need to include the normal vector to each vertex (based on the surface where the vertex is), update our vertex attributes and add it to the vertex shader as an input vec3 vertex attribute, and then we set an output variable to pass it onto the fragment shader, such as:
*vertex shader*
```glsl
[...]
layout (location = 0) in vec3 aPos;
layout (location = 1) in vec3 aNormal;

out vec3 Normal;

[...]
Normal = aNormal;
```
*fragment shader*
```
in vec3 Normal;
```

### Calculating diffuse
We have the normal vector but now we still need the light's position vector and the fragment's position vector. Since the light's position is a single static variable we can declare it as a uniform and pass it in the fragment shader:
```glsl
uniform vec3 lightPos;
```
And we update the light position in our C++ loop.

We also need the fragment position, which we can pass from our vertex shader, by multiplying the vertex position (`aPos`) with our model matrix, to take into account our transformations and do the lighting calculations in world space:
*vertex shader*
```glsl
out vec3 FragPos;
[...]
FragPos = vec3(model * vec4(aPos, 1.0));
```
*fragment shader*
```glsl
in vec3 FragPos;
```
This in variable will be interpolated from the 3 world position vectors of the triangle to form the `FragPos` vector that is the per-fragment world position.

**Light Direction vector**
The first thing we need to calculate is the direction vector between the light source and the fragment's position, which is simply to calculate the difference vector between the light position and the fragment's position.
```glsl
vec3 norm = normalize(Normal);
vec3 lightDir = normalize(lightPos - FragPos);
```
When calculating lighting it is important to always normalize the relevant vector to ensure they're actual unit vectors.

**Diffuse impact**
To calculate the diffuse impact we take the dot product between the `norm` and `lightDir` vectors. The result is then multiplied with the light's color to get the diffuse component:
```glsl
float diff = max(dot(norm, lightDir), 0.0);
vec3 diffuse = diff * lightColor;
```
If the angle between both vectors is greater than 90°, the dot product will be negative, so we need to take a `max` between the product and 0.

Now we simply combine the ambient and diffuse components and multiply the result with the color of the object:
```glsl
vec3 result = (ambient + diffuse) * objectColor;
gl_FragColor = vec4(result, 1.0);
```

**Normal matrix**
When passing in the normals, they get affected by the transformations in the model matrix as well. For example, if the model matrix would perform a non-uniform scale (different scale factors in each component) the vertices would be changed in such a way that the normal vector is not perpendicular to the surface anymore.
The trick of fixing this behavior is to use a different model matrix specifically tailored for normal vectors. This is called the *normal matrix* and uses some linear algebraic operations to remove the effect of wrongly scaling the normal vectors.

The normal matrix is defined as the transpose of the inverse of the upper-left 3x3 part of the model matrix. It can be calculated in the vertex shader using glsl functions:
```glsl
Normal = mat3(transpose(inverse(model))) * aNormal;
```
Inverting matrices is a costly operation for shaders, so it is best to calculate the normal matrix on the CPU and send it to the shaders via a uniform. But this will do for now.

## Specular lighting
Specular lighting is based on the light's direction vector and the object's normal vectors, but it is also based on the view direction (from what direction the observer is looking at the fragment). Specular lighting is based on the reflective properties of the surfaces. If we think of the object's surface as a mirror, the specular lighting is the strongest wherever we would see the light reflected on the surface.
![[Pasted image 20240708125233.png]]
We calculate a reflection vector by reflecting the light direction around the normal vector. Then we calculate the angular distance between this reflection and the view direction. The closer the angle between them, the greater the impact of the specular light. The resulting effect is that we see a bit of a highlight when we're looking at the light's direction reflected via the surface.

The view direction vector can be calculated using the viewer's world position and the fragment's position. Then we calculate the specular's intensity, multiply this with the light color and add this to the ambient and diffuse components.

The lighting calculations can also be done in view space, since the viewer's position in that space is always (0,0,0). It would just be needed to transform all the relevant vectors with the view matrix as well (and change the normal matrix too). But we'll stick to world space.

So we first take the position of the viewer (e.g. camera position) and pass it as a uniform to our shader:
```glsl
uniform vec3 viewPos;
```
Then we also set a specular intensity value (which is actually dependent on the material of the object):
```glsl
float specularStrength = 0.5;
```

Now we calculate the view direction vector and the corresponding reflect vector along the normal axis:
```glsl
vec3 viewDir = normalize(viewPos - FragPos);
vec3 reflectLightDir = reflect(-lightDir, norm);
```
Note that we negate `lightDir` when reflecting because it expects the first vector to point from the light source towards the frag's position, but it is currently the other way around (we calculated it with `lightDir - FragPos`), so we just need to negate it to get the expected direction.

Then we just need to calculate the specular component. This is accomplished by the following code:
```glsl
float spec = pow(max(dot(viewDir, reflectLightDir), 0.0), 32);
vec3 specular = specularStrength * spec * lightColor;
```

We first calculate the dot product between the view direction and the reflect direction and then raise it to the power of 32. This power value is the shininess value of the highlight. The higher the shininess value of an object, the more properly it reflects the light instead of scattering it all around and thus the smaller the highlight becomes.
![[Pasted image 20240708130445.png]]

The only thing left is to then combine the specular component with the other components:
```glsl
vec3 result = (ambient + diffuse + specular) * objectColor;
gl_FragColor = vec4(result, 1.0);
```

# Materials
In the real world each object has a different reaction to light and it mostly depends on the material its made. 
To simulate materials in OpenGL, we can use a struct to keep things organized:
```glsl
struct Material
{
	vec3 ambient;
	vec3 diffuse;
	vec3 specular;
	float shininess;
};

uniform Material material;
```
Each Phong lighting component is now defined as a 3d vector. The reason for this is that:
- The **ambient** material vector defines what color the surface reflects under ambient lighting (usually the same as the surface's color).
- The **diffuse** material vector defines the color of the surface under diffuse lighting (again set to the desired surface's color).
- The **specular** material vector sets the color of the specular highlight on the surface (or reflect a surface-specific color).
- The **shininess** impacts the scattering/radius of the specular highlight.

This [table](http://devernay.free.fr/cours/opengl/materials.html) contains some values for simulating real world materials.
![[Pasted image 20240709075908.png]]

To access the new Material struct, in the shader we simply use it as a common struct, like `material.ambient`, `material.diffuse`, etc. To pass our values from C++ to the Material uniform, we simply use the type of the property (such as vec3) and the name will also be `material.ambient`, `material.diffuse` etc.

## Light properties
Light sources also have different intensities for their ambient, diffuse and specular components. 
For example, the ambient component shouldn't be so strong so that it doesn't have such a big impact on the final color, so we can set it to a lower value (like `vec3(0.1)`). We can do the same for the diffuse and specular intensities. So we create a struct for the Light too:
```glsl
struct Light
{
	vec3 position;

	vec3 ambient;
	vec3 diffuse;
	vec3 specular;
};
uniform Light light;
```

- The **ambient** light is usually set to a low intensity because we don't want the ambient color to be too dominant.
- The **diffuse** component of a light source is usually set to the exact color we'd like a light to have (often a bright white color).
- The **specular** component is usually kept at `vec3(1.0)` shining at full intensity.

# Lighting maps
Using a unique material for each object is sufficient for the simplest models. But in the real world objects consists of several materials. So the material system above is not sufficient.
*Diffuse* and *specular maps* allow us to influence the diffuse (and indirectly the ambient component since they should be the same anyways) and the specular component of an object with much more precision.

## Diffuse maps
This makes it possible for us to set the diffuse color of an object for each individual fragment. This is just using textures.

To use a diffuse map in shaders we only need to pass the `diffuse` component of the material as a `sampler2D`:
```glsl
struct Material
{
	sampler2D diffuse;
	vec3 specular;
	float shininess;
};
[...]
in vec2 TexCoords;
```

Then we simply sample from the texture to retrieve the fragment's diffuse color value (and for the ambient as well since they're the same):
```
vec3 diffuse = light.diffuse * diff * vec3(texture(material.diffuse, TexCoords));
vec3 ambient = light.ambient * vec3(texture(material.diffuse, TexCoords));
```

## Specular maps
Similar to diffuse maps. It is important to mix diffuse and specular maps because some materials have different specular values in a same texture. A wood crate has their metal frame with high specular highlight, but the wood middle doesn't.
For example, using this texture as a diffuse map:
![[Pasted image 20240709092114.png]]
Requires a specular map for the steel borders:
![[Pasted image 20240709092130.png]]

The specular map is a black and white textuer and the intensity of the specular highlight comes from the brightness of each pixel in the image.

To use specular maps is the same as using diffuse maps:
```glsl
struct Material
{
	sampler2D diffuse;
	sampler2D specular;
	float shininess;
};
```

# Light casters
A light source that casts light upon objects is called a light caster. Most common types are directional light, point light (an extension of what we already did) and spotlight.

## Directional light
When a light source is far away the light rays coming from it are close to parallel to each other. It looks like all the light rays are coming from the same direction, regardless of where the object and/or the viewer is.

When a light source is modeled to be *infinetely* far away it is called a directional light since all its light rays have the same direction. It is independent of the location of the light source. The sun is an example of a directional light source.
![[Pasted image 20240710090454.png]]

We can model such a directional light by defining a light direction vector instead of using the light source's position:
```glsl
struct DirectionalLight
{
	vec3 direction;

	vec3 ambient;
	vec3 diffuse;
	vec3 specular;
};
[...]
void main()
{
	vec3 lightDir = normalize(-light.direction);
}
```
We negate the `light.direction` vector because all the lighting calculations we did so far expect the light direction to be a direction from the fragment towards the light source.

Directional lights are great for global lights that illuminate the entire scene.

## Point lights
A point light is a source with a given position somewhere in a world that illuminates in all directions, where the light rays fade out over distance.
![[Pasted image 20240710093304.png]]

### Attenuation
To reduce the intensity of light over the distance a light ray travels is called attenuation. 
The following formula calculates an attenuation value based on a fragment's distance to the light source, which we later multiply with the light's intensity vector:
$$
F_{att} = \frac{1.0}{K_c + K_l\cdot d + K_q \cdot d^2}
$$
- $d$ is the distance from the fragment to the light source
- $K_c$ is the *constant* term, usually kept at 1.0 which is mainly there to make sure the denominator never gets smaller than 1.
- $K_l$ is the *linear* term and is multiplied with the distance to reduce the intensity linearly
- $K_q$ is the *quadratic* term and is multiplied with the squared distance and sets a quadratic decrease of intensity for the light source.

Due to the quadratic term the light will diminish mostly linearly until the distance becomes light enough. The resulting effect is that the light is quite intense when at a close range, but quickly loses its brightness over distance:
![[Pasted image 20240710093928.png]]

**Choosing the right values**
Setting the right values for the 3 constants depends on a lot of factors, such as the environment, distance to cover, type of light, etc. The following table, extracted from [Ogre3D's wiki](http://www.ogre3d.org/tikiwiki/tiki-index.php?page=-Point+Light+Attenuation), shows some of the values these terms could take to simulate a (sort of) realistic light source that covers a specific radius (distance):
![[Pasted image 20240710094217.png]]

### Implementing attenuation and point light
We'll be using the light position and 3 new values for those constants:
```glsl
struct PointLight
{
	vec3 position;

	vec3 ambient;
	vec3 diffuse;
	vec3 specular;

	float constant;
	float linear;
	float quadratic;
};
```
And then we just need to calculate the distance from the fragment to the light source and the attenuation:
```glsl
float distance = length(light.position - FragPos);
float attenuation = 1.0 / (light.constant + light.linear * distance + light.quadratic * (distance*distance));
```
Then we apply this attenuation in every component of the light:
```glsl
ambient  *= attenuation;
diffuse  *= attenuation;
specular *= attenuation;
```


## Spotlight
A spotlight is a light source that is located somewhere in the environment that, instead of shooting light rays in all directions, only shoots them in a specific direction. A good example is a street lamp or a flashlight.

A spotlight in OpenGL is represented by a world-space position, a direction and a cutoff angle that specifies the radius of the spotlight. For each fragment we calculate if the fragment is between the spotlight's cutoff directions (thus in its cone) and if so, we lit the fragment accordingly.
![[Pasted image 20240710102336.png]]
- `LightDir`: the vector pointing from the fragment to the light source.
- `SpotDir`: the direction the spotlight is aiming at.
- $\phi$: the cutoff angle that specifies the spotlight's radius. Everything outside this angle is not lit by the spotlight.
- $\theta$: the angle between the `LightDir` vector and the `SpotDir` vector. The $\theta$ value should be smaller than $\phi$ to be inside the spotlight.

So basically we need to calculate the dot product between the (normalized) `LightDir` vector and the `SpotDir` vector and compare this with the cutoff angle $\phi$. 

### Flashlight
A flashlight is a spotlight located at the viewer's position and usually aimed straight ahead from the player's perspective. It's position and direction will be continually updated based on the player's position and orientation.

This is a basic model struct for a spotlight:
```glsl
struct SpotLight
{
	vec3 position;
	vec3 direction;
	float cutOff; // angle in radians

	vec3 ambient;
	vec3 diffuse;
	vec3 specular;

	float attConstant;
	float attLinear;
	float attQuadratic;
};
```

to use it as a flashlight we simply need to pass in:
```cpp
lightingShader.setVec3("light.position", camera.Position); lightingShader.setVec3("light.direction", camera.Front);
```

Now we just calculate the cosine of $\theta$ and compare it to our cosine of $\phi$ (we use cosine because the dot product will return a cosine and not the angle):
```glsl
float cosTheta = dot(lightDir, normalize(-light.direction));
float cosCutoff = cos(light.cutoff);

if (cosTheta > cosCutoff)
{
	// do lighting calculations
}
else
{
	// use ambient light only
	color = vec4(light.ambient * vec3(texture(material.diffuse, TexCoord)), 1.0)
}
```

We also need to calculate the attenuation using the passed constants, since the same intensity decrease applies for a spotlight.

### Smooth/Soft edges
To create the effect of a smoothly-edged spotlight we want to simulate a spotlight having an inner and an outer cone. The inner one can be the one already defined before, the outer one needs to be defined so it gradually dims the light from the inner to the edges of the outer cone.

To create an outer cone we define another angle between the spotlight's direction vector and the outer cone's vector. Then if a fragment is between the inner and the outer cone it calculates an intensity value between 0.0 and 1.0. If the fragment is inside the inner cone its intensity is equal to 1.0 and 0.0 if the fragment is outside the outer cone.
To calculate the intensity we use this formula:
$$
I = \frac{\theta - \gamma}{\epsilon}
$$
- $\theta$ is the angle between the fragment-light direction vector and the spotlight direction vector.
- $\gamma$ is the angle of the outer cone
- $\epsilon$ is the difference between the inner ($\phi$) and the outer cone ($\gamma$): $\epsilon = \phi - \gamma$.

## Using multiple lights
The main workflow here will be to calculate each light in separate GLSL functions and then add them all together in the final result.


# Model Loading - Assimp
Instead of manually defining all the vertices, normals and texture coordinates for every mesh we want to draw, we can import 3D models from external softwares (such as Blender). Those 3D models allows us to create complicated shapes and apply textures to them via a process called uv-mapping, and the vertex coordinates, vertex normals and texture coordinates will be automatically generated.

## Assimp
Assim (Open Asset Import Library) is a very popular model importing library that is able to import dozens of different model file formats by loading all the data into Assimp's generalized data structures.

When importing a model via Assimp, it loads the entire model into a scene object that contains all the data of the imported model/scene. This is a simplistic model of Assimp's structure:
![[Pasted image 20240713230820.png]]
- All the data of the scene/model is contained in the ***Scene*** object like all the materials and meshes. It also contains a reference to the root node of the scene
- The ***Root Node*** of the scene may contain children nodes (all the other nodes as well) and could have a set of indices that point to mesh data in the scene object's `mMeshes` array. The scene's `mMeshes` array contains the actual Mesh objects. *The values in the `mMeshes` array of a node are only indices for the scene's meshes array*.
- A ***Mesh*** object itself contains all the relevant data required for rendering, such as vertex positions, normal vectors, texture coordinates, faces, and the material of the object.
- A mesh contain several faces. A ***Face*** represents a render primitive of the object (triangles, quads, points). A face contains the indices of the vertices that form a primitive, which makes it easy to render via an index buffer.
- A mesh also links to a ***Material*** object that hosts several functions to retrieve the material properties of an object. Like colors and/or texture maps.

The basic workflow is: load an object into a ***Scene*** object, recursively retrieve the corresponding ***Mesh*** objects from each of the nodes (we recursively search each node's children) and process each ***Mesh*** object to retrieve the vertex data, indices and its material properties. The result is then a collection of mesh data that we want to contain in a single `Model` object.

Based on the [Model](https://learnopengl.com/Model-Loading/Model) chapter of LearnOpenGL, the basic workflow of importing a 3D model into OpenGL with Assimp is based in four "simple" functions:
```cpp
// Assimp include files:
#include <assimp/Importer.hpp>
#include <assimp/scene.h>
#include <assimp/postprocess.h>


void loadModel(const std::string& path);
void processNode(aiNode* node, const aiScene* scene);
Mesh processMesh(aiMesh* mesh, const aiScene* scene);
std::vector<Texture> loadMaterialTextures(aiMaterial* mat, aiTextureType type);
```
with `Mesh` and `Texture` being custom classes we built and we convert assimp's mesh and texture to our type in those functions.

`loadModel` implementation looks a bit like this:
```cpp
void loadModel(string path) 
{ 
	Assimp::Importer import; 
	const aiScene *scene = import.ReadFile(path, aiProcess_Triangulate | aiProcess_FlipUVs); 
	
	if(!scene || scene->mFlags & AI_SCENE_FLAGS_INCOMPLETE || !scene->mRootNode) 
	{ std::cerr << "ERROR::ASSIMP::" << import.GetErrorString() << endl; return; 
	} 
	
	processNode(scene->mRootNode, scene); 
	
}
```
These post-processing flags in our `Assimp::Importer::ReadFile` call deserves extra attention. They allows us to specify several options that forces Assimp to do extra calculations/operations on the imported data, some of them are:
- `aiProcess_Triangulate`: If Assimp loads a model that does not (entirely) consists of triangles, it should transform all that model's primitives shapes to triangles first.
- `aiProcess_FlipUVs`: flips the texture coordinates on the y-axis where necessary (most images in OpenGL end up reversed so it's necessary).
- `aiProcess_GenNormals`: creates normal vectors for each vertex if the model doesn't contain normal vectors.
- `aiProcess_SplitLargeMeshes`: splits large meshes into smaller sub-meshes which is useful if there is a maximum number of vertices allowed per mesh.
- `aiProcess_OptimizeMeshes`: does the reverse by trying to join several meshes into one larger mesh, reducing drawing calls for optimization.
- and many more that are really useful can be found [here](https://github.com/assimp/assimp/blob/master/include/assimp/postprocess.h).

`processNode` implementation looks like this:
```cpp
void processNode(aiNode* node, const aiScene* scene)
{
	// process all node's meshes (if any)
    for (unsigned int i = 0; i < node->mNumMeshes; i++)
    {
		// get mesh based on the index in mMeshes of the node
		aiMesh* mesh = scene->mMeshes[node->mMeshes[i]];
		// build our mesh and add to this model
		m_meshes.push_back(processMesh(mesh, scene));
    }
	// then recursively do the same for each of its children
    for (unsigned int i = 0; i < node->mNumChildren; i++)
    {
		processNode(node->mChildren[i], scene);
    }
}
```
We recursively check for each of the node's mesh by accessing it's mesh indices and retrieving the corresponding mesh from our scene root node, and then do it for all of its children until there's no more.

The `processMesh` function then takes care of converting Assimp's mesh to our custom Mesh, which is essentially a struct of Vertices (which is by itself a sturct of vec3 position, vec3 normals and vec2 texcoords), Indices and Textures. It's implementation looks like:
```cpp
Mesh Model::processMesh(aiMesh* mesh, const aiScene* scene)
{
    std::vector<Vertex> vertices;
    std::vector<unsigned int> indices;
    std::vector<Texture> textures;

    // process each mesh vertex
    for (unsigned int i = 0; i < mesh->mNumVertices; i++)
    {
	Vertex vertex{};

	// process mesh vertices
	glm::vec3 vector;
	vector.x = mesh->mVertices[i].x;
	vector.y = mesh->mVertices[i].y;
	vector.z = mesh->mVertices[i].z;
	vertex.Position = vector;

	// process mesh normals
	vector.x = mesh->mNormals[i].x;
	vector.y = mesh->mNormals[i].y;
	vector.z = mesh->mNormals[i].z;
	vertex.Normal = vector;

	// process texture coordinates
	// assimp allows models to have up to 8 different TexCoords
	// per vertex. but (for some reason) we only care about 1
	if (mesh->mTextureCoords[0]) // check if has TexCoords
	{
	    glm::vec2 vec;
	    vec.x = mesh->mTextureCoords[0][i].x;
	    vec.y = mesh->mTextureCoords[1][i].y;
	    vertex.TexCoords = vec;
	}
	else 
	{
	    vertex.TexCoords = glm::vec2(0.0f, 0.0f);
	}

	vertices.push_back(vertex);
    }

    // process each mesh index
    for (unsigned int i = 0; i < mesh->mNumFaces; i++)
	{
		aiFace face = mesh->mFaces[i];
		for (unsigned int j = 0; j < face.mNumIndices; j++)
		    indices.push_back(face.mIndices[j]);
    }

    // process mesh materials
    if (mesh->mMaterialIndex >= 0)
    {
	aiMaterial* material = scene->mMaterials[mesh->mMaterialIndex];

	// first take diffuse maps
	std::vector<Texture> diffuseMaps = loadMaterialTextures(material, aiTextureType_DIFFUSE);

	textures.insert(textures.end(), diffuseMaps.begin(), diffuseMaps.end());

	// now take specular maps
	std::vector<Texture> specularMaps = loadMaterialTextures(material, aiTextureType_SPECULAR);
	textures.insert(textures.end(), specularMaps.begin(), specularMaps.end());
    }

    return Mesh(vertices, indices, textures);
}
```

Then lastly we call `loadMaterialTextures` which parses Assimp's texture types to our own. Note that our Texture type is a structure containing an Id and our texture type (DIFFUSE or SPECULAR). It's implementation looks like:
```cpp
std::vector<Texture> Model::loadMaterialTextures(aiMaterial* mat, aiTextureType type)
{
    std::vector<Texture> textures;
    for (unsigned int i = 0; i < mat->GetTextureCount(type); i++)
    {
		aiString str;
		mat->GetTexture(type, i, &str);
	
		bool skip = false;
		for (unsigned int j = 0; j < g_loadedTextures.size(); j++)
		{
		    if (std::strcmp(g_loadedTextures[j].Path.c_str(), str.C_Str()) == 0)
		    {
			textures.push_back(g_loadedTextures[j]);
			skip = true;
			break;
		    }
		}
		if (skip)
		    continue;
	
		Texture texture;
		texture.Id = TextureFromFile(str.C_Str(), m_directory);
		
		switch (type)
		{
		case (aiTextureType_DIFFUSE):
		    texture.Type = TextureType::DIFFUSE;	
		    break;
	
		case (aiTextureType_SPECULAR):
		    texture.Type = TextureType::SPECULAR;
		    break;
	
		// just to get rid of warnings
		default:
		    texture.Type = TextureType::DIFFUSE;
		}
		
		texture.Path = str.C_Str();
	
		textures.push_back(texture);
		g_loadedTextures.push_back(texture);
    }

    return textures;
}
```
In this function, `g_loadedTextures` is a global variable we maintain to keep track of every path loaded to avoid loading the same texture more than once.


# Depth testing
The depth buffer (or z-buffer) is a buffer that, just like the *color buffer* (which stores all the fragment colors: the visual output, that's why we clear it at the start of every frame), stores information per fragment and has the same width and height as the color buffer. It is automatically created by the windowing system and stores its depth values as 16, 24 or 32 bit floats.

When depth testing is enabled, OpenGL testes the depth value of a fragment against the content of the depth buffer, and if the test passes, the fragment is rendered and the depth buffer is updated. If it fails, the fragment is discarded.

Depth testing is done in screen space after the fragment shader has run. The screen space coordinates relate directly to the viewport defined by OpenGL's `glViewport` and can be accessed via GLSL's built-in `gl_FragCoord` variable in the fragment shader. The x and y components of `gl_FragCoord`represent the fragment's screen-space coordinates (with 0,0 being the bottom-left corner) and the z-component contains the depth value of the fragment.

Most GPUs nowadays support *early depth testing*, which allows the depth test to run before the fragment shader runs (fragment shaders are usually quite expensive).

Enabling depth testing is simple like we did before:
```cpp
glEnable(GL_DEPTH_TEST);
```
Then OpenGL automatically stores fragment's z-values in the depth buffer if they passed the test, otherwise discard them. It is necessary to clear the depth buffer at the beginning of every frame as well:
```cpp
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
```

## Depth test function
OpenGL allows us to modify the comparison operators/depth func it runs in the depth test. This allows us to control when OpenGL should pass or discard fragments and when to update the depth buffer. We can set that by calling `glDepthFunc`:
```cpp
glDepthFunc(GL_LESS);
```
The comparisons this functions accepts are:
- `GL_ALWAYS`: The depth test always passes.
- `GL_NEVER`: The depth test never passes.
- `GL_LESS`: Passes if the fragment's depth value is less than the stored depth value.
- `GL_EQUAL`: Passes if the fragment's depth value is equal to the stored depth value
- `GL_LEQUAL`: Passes if it's less than or qual to the stored depth value
- `GL_GREATER`: Passes if it's greater than
- `GL_NOTEQUAL`
- `GL_GEQUAL`

By default the depth function is `GL_LESS`, which means that every fragment that has a depth value higher than or equal to the current depth buffer's value is discarded.

## Depth value precision
The depth buffer contains depth values between 0.0 and 1.0 and it compares its content with the z-values of all the objects in the scene as seen from the viewer. These z-values in view space can be any value between the projection-frustum's Near and Far planes. 
A transform function then takes these view-space z-values and transforms them to the range [0, 1]. 

One such function is a linear transform:
$$
F_{depth}(z) = \frac{z - near}{far - near}
$$
which gives us a linear relation between the z-value and its corresponding depth value:
![[Pasted image 20240720145424.png]]
But because of the way projection is calculated, linear depth buffer is almost never used. 

A non-linear depth equation proportional to 1/z is much more useful. Z-values between 1.0 and 2.0 account for 50% of the depth values in range [0,1], while z-values between 50.0 and 100.0 account only for 2% of the range. The result is that we get much more depth precision to the objects close by. Such equation is:
$$
F_{depth}(z) = \frac{1/z - 1/near}{1/far - 1/near}
$$
![[Pasted image 20240720145921.png]]

The effect of this equation can be seen by visualizing the depth-buffer. Since the z-value of the built-in shader variable `gl_FragCoord` contains the depth value of the fragment, we can output that depth value as our color:
```glsl
gl_FragColor = vec4(vec3(gl_FragCoord.z), 1.0);
```
![[Pasted image 20240720150442.png]]
The closer an object is, the darker its color gets, because it's depth value approaches 0.

## Z-fighting 
Z-fighting occurs when two objects are too close to each other and so the depth buffer does not have enough precision to figure out which one of the two shapes is in front of each other. The result is that the two shapes continually seem to switch order which causes weird glitchy patterns:
![[Pasted image 20240720152053.png]]
Preventing z-fighting from happening completely is impossible. But there are a few tricks to minimize it as possible as we can:
- Never place objects too close to each other in a way that some of their triangles closely overlap.
- Set the near plane as far as possible from the viewer. This has to be done carefully so it doesn't cause undesired clipping
- At the cost os some performance, use a higher precision depth buffer (usually its 24 bits, but most GPUs also support 32 bits depth values).


# Stencil Testing
Once the fragment shader has processed, a *stencil test* is executed that has the option to discard fragments. After that the remaining fragments are passed to the depth test.

The stencil test is based on the content of yet another buffer called ***stencil buffer*** that we're allowed to update during rendering to achieve different effects.
A stencil buffer (usually) contains 8 bits per stencil value (range of 0 to 255). We can set this custom and we can discard or keep fragments based on that stencil value.

GLFW creates the stencil buffer automatically.
An example of using stencil buffer:
![[Pasted image 20240725104442.png]]
The stencil buffer is first cleared with zeros and then we set a rectangle of 1s in the buffer. Then we only render the fragments which stencil value is 1.

The general workflow with using stencil buffers is:
- Enable writing to the stencil buffer:
- Render objects, updating the content of the stencil buffer.
- Disable writing to the stencil buffer.
- Render (other) objects, this time discarding certain fragments based on the content of the stencil buffer.

Enabling stencil buffer writing is pretty simple:
```cpp
glEnable(GL_STENCIL_TEST);

// ... then inside the loop we have to clear the buffer too
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT | GL_STENCIL_BUFFER_BIT);
```
then we can set the stencil buffer's *mask* as well with `glStencilMask`, that allows us to set a bitmask that is ANDed with the stencil value about to be written, e.g.:
```cpp
glStencilMask(0xFF); // each bit is written to the stencil buffer as is
glStencilMask(0x00); // each bit ends up as 0 in the stencil buffer (disable writes)
```

**Stencil Functions**:
Similar to depth testing with its different functions, we can configure the test that runs in the stencil test. Two functions are used to configure stencil testing: `glStencilFunc` and `glStencilOp`.

`glStencilFunc(GLenum func, GLint ref, GLuint mask)`:
- `func`: sets the stencil function that determines whether a fragment passes or is discarded based on its stencil value and compared to the `ref` value. Possible options (just like in depth test) are: `GL_NEVER, GL_LESS, GL_LEQUAL, GL_GREATER, GL_GEQUAL, GL_EQUAL, GL_NOTEQUAL, GL_ALWAYS`.
- `ref`: specifies the reference value for the stencil test to compare the stencil buffer's content with.
- `mask`: specifies that mask that is ANDed with both the reference value and the stored stencil value before the test compares them.

So in the case of the example in the image, the function would be set to:
```cpp
glStencilFunc(GL_EQUAL, 1, 0xFF);
```
This tells OpenGL that whenever the (stencil value & 0xFF) is equal (GL_EQUAL) to the reference value (1 & 0xFF) the fragment passes the test and is drawn, otherwise discarded.

The function `glStencilOp` then allows us to specify how OpenGL should update the stencil buffer values.
`glStencilOp(GLenum sfail, GLenum dpfail, GLenum dppass)`:
- `sfail`: action to take if the stencil test fails
- `dpfail`: action to take if the stencil test passes, but the depth test fails
- `dppass`: action to  take if both the stencil test and depth test fails
then for each option these are the possible action values:
- `GL_KEEP`: the currently stored stencil value is kept.
- `GL_ZERO`: the stencil value is set to 0.
- `GL_REPLACE`: the stencil value is replaced with the reference value set with `glStencilFunc`.
- `GL_INCR`: the stencil value is increased by 1 if its lower than the maximum value.
- `GL_INCR_WRAP`: same as `GL_INCR` but wraps it back to 0 when maximum value is exceeded.
- `GL_DECR`: decreases stencil value by 1 if higher than the minimum value.
- `GL_DECR_WRAP`: same as `GL_DECR` but wraps it to the maximum value if it ends up lower than 0.
- `GL_INVERT`:  bitwise inverts the current stencil buffer value.

By default `glStencilOp` is set to `GL_KEEP, GL_KEEP, GL_KEEP` which specifies that the stencil buffer will always keep its values. It does not update the stencil buffer ever, so if we want to write to it we need to specify at least one different action.

### Usage demonstration: Object outlining
![[Pasted image 20240725111058.png]]
To create such effect of an "outlining border" we follow this routine:
1. Enable stencil writing
2. Set stencil op to `GL_ALWAYS` before drawing the objects which will be outlined, updating the stencil buffer with 1s wherever the object's fragments are rendered.
3. Render the objects.
4. Disable stencil writing and depth testing.
5. Scale each of the objects by a small amount.
6. Use a different fragment shader that outputs a single (border) color.
7. Draw the objects again, but only if their fragment's stencil values are not equal to 1 (which means that it is a fragment that does not contain an object's fragment).
8. Enable depth testing again and restore stencil func to `GL_KEEP`.
This process sets the content of the stencil buffer to 1s for each of the object's fragments and when we want to draw the borders, we draw scaled-up versions of the objects only where the stencil test passes. We're discarding all the fragments of the scaled-up versions that are part of the original object's fragment using the stencil buffer.

First we create a basic fragment shader that outputs a single border color:
```glsl
uniform vec3 u_borderColor;

void main()
{
	gl_FragColor = vec4(u_borderColor, 1.0);
}
```

For the objects we want to outline, we need to first draw them normally (while writing to the stencil buffer), disable writing and depth test, set the stencil func to test, and then write the scaled-up containers:

First we enable stencil testing:
```cpp
glEnable(GL_STENCIL_TEST);
```
In each start of frame we specify the actions to take for the stencil buffer writing:
```cpp
glStencilOp(GL_KEEP, GL_KEEP, GL_REPLACE);
```
This specifies that whenever both the stencil test and depth test succeed, we want to replace the stored stencil value with the reference value set via `glStencilFunc`.

We clear the stencil buffer at the start of the frame (to 0s) and update the stencil buffer (to 1s) for each fragment of the objects:
```cpp
glStencilOp(GL_KEEP, GL_KEEP, GL_REPLEACE);
glStencilFunc(GL_ALWAYS, 1, 0xFF);
glStencilMask(0xFF);
normalShader.Use();
DrawObjects();
```
Now the stencil buffer is updated with 1s where the objects were drawn. Now we draw the upscaled objects but this time we use the use the appropriate test function and disable writing to the stencil buffer:
```cpp
glStencilFunc(GL_NOTEQUAL, 1, 0xFF);
glStencilMask(0x00); // disable writing
glDisable(GL_DEPTH_TEST);
outlineSingleColorShader.Use();
DrawScaledUpObjects();
```
Here we use stencil function `GL_NOTEQUAL` to only draw parts of the objects that are not equal to 1. 

Later we need to enable stuff back to normal again:
```cpp
glStencilMask(0xFF); // enable writing again
glStencilFunc(GL_ALWAYS, 1, 0xFF);
glEnable(GL_DEPTH_TEST);
```

