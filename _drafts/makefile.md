---
layout: post
title: A Simple Makefile
---

Compiles [C++11](http://zachwhaley.me/2014/02/20/cc11.html) code.

Uses a simple directory structure:
./    - Makefile and executable
./src - .cpp and .hpp files
./obj - Generated .o and .d files

```make
CXX = g++
CXXFLAGS = -g -Wall -std=c++11
LIBS = # -lncurses

PROJECT = project
SRCDIR = src
OBJDIR = obj
SOURCES = $(wildcard $(SRCDIR)/*.cpp)
OBJECTS = $(patsubst $(SRCDIR)/%.cpp, $(OBJDIR)/%.o ,$(SOURCES))

.PHONY: all clean

all: $(PROJECT)

$(OBJECTS): | $(OBJDIR)

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(PROJECT): $(OBJECTS)
	$(CXX) $(OBJECTS) $(LIBS) -o $(PROJECT)

$(OBJDIR)/%.o: $(SRCDIR)/%.cpp
	$(CXX) $(CXXFLAGS) -MMD -c $< -o $@

clean:
	rm -f -r $(OBJDIR) $(PROJECT)
```

Use GNU's C++ compiler
Use these flags are used when compiling source code to object files.
-g Requests debugging information
-Wall Turns on all compile warnings
-std=c++11 Specifies the code is C++11
Add any libraries needed for the project
Each library starts with a -l, e.g. ncurses below.

The project executable's name.
The source directory where your .cpp and .hpp files are located.
The object directory where your .o and .d files are going to go.
Creates a list of your source files.
Creates a list of object files to create.

Ignores any files named all or clean when calling 'make clean'

The Makefile's main function.

Create the object directory if none of the object files exist yet.
The | means $(OBJDIR) must happen before $(OBJECTS)

Make the object directory

Make the project executable
-o Sets the name of the executable

Make an object file for each source file
-MMD Creates dependency files for dependencies.
-c $< Compiles the source file.  $< is the name on the right of the :
-o $@ Sets the compiled objects name. $@ is the name on the left of the :

Removes compiled files.

```bash
$ make # Compiles your code
$ make clean # Removes compiled files.
```

I'm still new to Make; see something wrong?  [Let me know :-)](https://gist.github.com/zachwhaley/9458612)
