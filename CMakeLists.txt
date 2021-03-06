cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
cmake_policy(SET CMP0048 NEW)
set(CMAKE_C_STANDARD 11)
set(PACKAGE_VERSION 1.0)
set(PACKAGE_BUGREPORT https://github.com/EZ3CHI3L/Eternity/issues)
include(GNUInstallDirs)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -Wall -Werror -g")
project(eternity VERSION ${PACKAGE_VERSION} LANGUAGES C)

if (BUILD_TESTING)
    enable_testing()
    find_package(cmocka 1.1.1 CONFIG REQUIRED)
    if (CMOCKA_FOUND)
        include_directories(${CMOCKA_INCLUDE_DIRS})
        link_libraries(${CMOCKA_LIBRARIES})
    endif (CMOCKA_FOUND)
endif (BUILD_TESTING)

find_package(OpenGL REQUIRED)
if (OPENGL_FOUND)
    include_directories(${OPENGL_INCLUDE_DIRS})
    link_libraries(${OPENGL_LIBRARIES})
endif (OPENGL_FOUND)

find_package(glfw3 3.2 REQUIRED)
if (GLFW_FOUND)
    include_directories(${GLFW_INCLUDE_DIRS})
    link_libraries(${GLFW_LIBRARIES})
endif (GLFW_FOUND)

find_package(GLEW 2.0 REQUIRED)
if (GLEW_FOUND)
    include_directories(${GLEW_INCLUDE_DIRS})
    link_libraries(${GLEW_LIBRARIES})
endif (GLEW_FOUND)

add_subdirectory(src)

SET(CPACK_GENERATOR "DEB")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "Ezechiel Ethan Sealover") #required
INCLUDE(CPack)
