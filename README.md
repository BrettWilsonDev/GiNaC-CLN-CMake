# GiNaC + CLN CMake Build

This repository provides a combined build of **GiNaC** and **CLN**, allowing you to easly build them together and use them via CMake.

## Using This Repository in Your CMake Project

You can include this repository using `FetchContent`:

```cmake
include(FetchContent)

FetchContent_Declare(GiNaCBuild
    GIT_REPOSITORY https://github.com/BrettWilsonDev/GiNaC-CLN-CMake.git
    GIT_TAG master
    GIT_SHALLOW TRUE
    GIT_PROGRESS TRUE
)

FetchContent_MakeAvailable(GiNaCBuild)
FetchContent_GetProperties(GiNaCBuild)

# Example: link GiNaC + CLN to your target
# Replace <YourTarget> with the actual target in your project
target_link_libraries(<YourTarget> PRIVATE GiNaCBuild)
```

This will automatically fetch, build, and make GiNaC + CLN available in your project.

## License
This repository combines GiNaC and CLN for convenience.  
Both projects are licensed under the GNU General Public License (GPL).  

- GiNaC is licensed under GPLv2 (or later).  
- CLN is licensed under GPLv2 (or later).  

All original copyright notices are preserved.  
