# The Flutter tooling requires that developers have CMake 3.10 or later
# installed. You should not increase this version, as doing so will cause
# the plugin to fail to compile for some customers of the plugin.
cmake_minimum_required(VERSION 3.10)

project(jolt_physics_ffi_library VERSION 0.0.1 LANGUAGES C)

add_library(jolt_physics_ffi SHARED
  "jolt_physics_ffi.c"
)

set_target_properties(jolt_physics_ffi PROPERTIES
  PUBLIC_HEADER jolt_physics_ffi.h
  OUTPUT_NAME "jolt_physics_ffi"
)

target_compile_definitions(jolt_physics_ffi PUBLIC DART_SHARED_LIB)

if (ANDROID)
  # Support Android 15 16k page size
  target_link_options(jolt_physics_ffi PRIVATE "-Wl,-z,max-page-size=16384")
endif()
