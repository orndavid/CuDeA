# CuDeA
Core engine for mathematical calculations

## Objective
A base

## Build Methods
The build relies on CMake, version >3.16. The build was tested and built on Linux, Ubuntu 18.04.1. 
Once you have confirmed that the dependencies are met you create a build directory and use cmake to build it
```shell
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=release
make  #alternatively make -j8
```
This will create several libraries in the library/ folder.

## Benchmarking
A set of benchmarks was created for development, these benchmark codes can be found in the bench/ folder where a CMakeLists.txt file exists to build them if so requested. To build configure dependencies by git cloning the Googlebenchmark into the extern folder. Then clone the googletest into Googlebenchmark as suggested [here](https://github.com/google/benchmark#installation).
Once the dependencies have been dowloaded you should be able to run
```shell
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=bench
make # alternatively make -j8
```
Under folder build/bench/ there are the benchmarks as posted in bench/ folder.

## Testing
The testing requires googletest. If you want to test but not benchmark then create a folder in extern/
```shell
mkdir extern/ && cd extern
mkdir benchmark
git clone https://github.com/google/googletest.git benchmark/googletest
cd ../build/
cmake .. -DCMAKE_BUILD_TYPE=test
make # alternatively make -j8 
cd test/
```
This is because the benchmark relies on the googletest framework, so rather than have the build system detect that we just assume you want to benchmark.
Under the folder build/tests/ all the tests, as defined in tests/ can be found and run individually.
## Dependency libraries
The STD library is used extensively for containers and base algorithms. This is by choice to remove as many dependencies as posible.

- Current linear algebra library used is the armadillo library


## Quickly on the philosophy
We chose to create multiple smaller libraries so that the user can pick and choose which libraries to use. The objective here is to cover a wide range of possibilities in computation so many of the methods won't be overlapping. I.e. if you are doing some statistical analysis you don't need the libraries from another unreleated domain, e.g. complex analysis. 
So rather than create a monolith we create several smaller libraries which can be called. 
The current solution still builds all the libraries, that's just because they currently aren't so large. However in the future we might setup a configuration where the user can select which libraries to use as to reduce the overhead on the local machine.
