cmake_minimum_required(VERSION 3.22)

project(PluginTemplate LANGUAGES C CXX)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Clone JUCE framework from https://github.com/juce-framework/JUCE
# Configure the JUCE root path via an environment variable. Here JUCE_LIB is assumed to be this one.
# JUCE_LIB must point to the JUCE source root (the one containing CMakeLists.txt and modules/

# If (JUCE_LIB EXISTS)

    # Add JUCE as a subdirectory and keep its build artifacts out of the main tree
# ELSE
    # Download JUCE using FetchContent

if(DEFINED ENV{JUCE_LIB} AND NOT EXISTS "$ENV{JUCE_LIB}/modules")
  message(FATAL_ERROR
    "JUCE_LIB is set to '$ENV{JUCE_LIB}', but that does not look like the JUCE source root (missing 'modules/' folder)."
  )
endif()

if(DEFINED ENV{JUCE_LIB} AND EXISTS "$ENV{JUCE_LIB}/CMakeLists.txt")

  message(STATUS "JUCE: using local checkout at $ENV{JUCE_LIB}")
  set(JUCE_LOCAL_SOURCE "$ENV{JUCE_LIB}")
  add_subdirectory("${JUCE_LOCAL_SOURCE}" "${CMAKE_BINARY_DIR}/_deps/juce-build" EXCLUDE_FROM_ALL)

else()
  message(STATUS "JUCE: fetching via FetchContent")

  include(FetchContent)
  FetchContent_Declare(JUCE
    GIT_REPOSITORY https://github.com/juce-framework/JUCE.git
    GIT_TAG        8.0.11
  )
  # By default, FetchContent uses ${CMAKE_BINARY_DIR}/_deps for sources/builds.
  FetchContent_MakeAvailable(JUCE)
endif()

add_subdirectory(PluginTemplate)