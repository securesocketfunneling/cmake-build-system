## Introduction
This module offers a set of **CMake** helpers that can be use to ease several
tasks while defining a project.

## Features
Currently, the available features are:

* CMakeModules:
This feature is a large set of helpers offered by an external developer named
Ryan Palvik.

* [Externals](external-packages/README.md):
This feature helps to build external dependencies.

* Miscellaneaous:
This feature is a library of helpers to ease definition and integration of self
defined projects.

## Usage
To use this set of helpers, some modifications are needed in the **CMake** based
project. This is performed through two steps:
* [Reference sub-module](#reference-sub-module)
* [Update Modules Search Path](#update-modules-search-path)

### Reference sub-module
In order for the targeted **CMake** based Project to use **CMakeCommon**'s
helpers, it must first reference it.

This is easily performed thanks to **git**'s *submodule* feature:
```sh
# Go to the project's root path
cd targeted_project

# Add CMakeCommon sub-module.
# Note
#   We choose, here, to link sub-module under path 'cmake' located in the root
#   of the project.
git submodule add -b develop "repo_url/cmake-common.git" cmake

# Ensure all CMakeCommon's sub-modules are checked-out
git submodule update --init --recursive cmake
```

### Update Modules Search Path
Once the **CMakeCommon** module is available from the targeted project's source
tree, it must be initialized from a *CMakeLists.txt* list of the project. Just
add the following lines:
```cmake
# Initialize sub-module CMakeCommon that is linked on project's root
add_subdirectory(${CMAKE_SOURCE_DIR}/cmake)
```
> **Note**
>
> It is recommended to initialize the **CMakeCommon** module from the root
> *CMakeLists.txt* file. That will ensure the module's helpers are available to
> all of the other project's *CMakeLists.txt* files.