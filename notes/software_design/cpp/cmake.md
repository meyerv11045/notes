# Cmake

- Build tool for C and C++
- **Target**- the binary executable we want to build source code into
- **Properties**- anything such as compiler options and dependencies needed to create the target 
- `cmake_minimum_required(VERSION <version-num>) ` specifies the minimum cmake version to use
    - Modern CMAKE is 3.0+

```cmake
project (<project-name>
					VERSION 1.0
					DESCRIPTION "stuff"
					LANGUAGES CXX)
          # CXX stands for Cpp
```

``` cmake
add_executable(<name> 
	src/file1.h 
	src/file1.cpp 
	… )
```

``` cmake
target_compile_features(<exe-name> PRIVATE cxx_std_20) #private makes it not able to be included as a library
```

## Dependency Management

- `find_library(LIBRARY_SDL, sdl)` will search your system for a `sdl` named library and will store the path in `LIBRAY_SDL`

``` cmake
find_library(LIBRARY_SDL, sdl)
if (LIBRARY_SDL)
  target_link_libraries(myApp PRIVATE ${LIBRARY_SDL})
else()
	# throw an error or enable compilation without the library
endif()
```

- `find_package(<pkg-name>)` is better than find_library and can load CMAKE modules