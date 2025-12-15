# Audio-Plugin-Template

## Description

In this audio plugin template:

If the environment variable **JUCE_LIB** is defined, the project uses a local JUCE source checkout.

Otherwise, JUCE is fetched via CMake’s FetchContent and built as part of the project: `build/_deps/juce-src` (sources) and `build/_deps/juce-build` (build artifacts).

In both cases, JUCE is built from source and its modules are statically linked into the plugin.


## Debug:
```
cmake -B build
cmake --build build
```

## Release:
```
cmake -B build
cmake --build build --config Release
```