cmake_minimum_required(VERSION 3.27)
project(SDL2_example)

# SDL
list(APPEND CMAKE_PREFIX_PATH
     "${CMAKE_SOURCE_DIR}/external/SDL/SDL2-2.28.3/cmake")
find_package(SDL2)

add_executable(${PROJECT_NAME} src/main.cpp)
# SDL2::SDL2main may or may not be available. It is e.g. required by Windows GUI
# applications
if(TARGET SDL2::SDL2main)
  # It has an implicit dependency on SDL2 functions, so it MUST be added before
  # SDL2::SDL2 (or SDL2::SDL2-static)
  target_link_libraries(${PROJECT_NAME} PRIVATE SDL2::SDL2main)
endif()

# Link to the actual SDL2 library. SDL2::SDL2 is the shared SDL library,
# SDL2::SDL2-static is the static SDL libarary.
target_link_libraries(${PROJECT_NAME} PRIVATE SDL2::SDL2)
