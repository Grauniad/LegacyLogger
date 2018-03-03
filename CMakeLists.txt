set(CMAKE_PREFIX_PATH /home/lhumphreys/dev_tools_build/lib/cmake)
find_package(OSDevTools 0.1 REQUIRED)
find_package(UtilTime 0.1 REQUIRED)
#
# Project Definition
#
cmake_minimum_required(VERSION 3.8.2)
project(DevToolsLog)

#
# Exported Library (libLog)
#
add_library(Log STATIC
    src/logger.cpp
    include/logger.h
    include/logger_preProcessor.h
)
target_include_directories(Log PUBLIC
    $<BUILD_INTERFACE:${DevToolsLog_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
target_link_libraries(Log PRIVATE
    OSDevTools::OSDevTools
    UtilTime::Time
)

#
# Installation instructions
#
install(TARGETS Log EXPORT DevToolsLogTargets
    ARCHIVE  DESTINATION lib
    INCLUDES DESTINATION include
    PUBLIC_HEADER DESTINATION include
)

install (EXPORT DevToolsLogTargets
    FILE         DevToolsLogTargets.cmake
    NAMESPACE    DevToolsLog::
    DESTINATION  lib/cmake/DevToolsLog
)

#
# Define our package version
#
include(CMakePackageConfigHelpers)
write_basic_package_version_file("DevToolsLogConfigVersion.cmake"
    VERSION       0.1
    COMPATIBILITY SameMajorVersion
)
install (
    FILES       ${DevToolsLog_BINARY_DIR}/DevToolsLogConfigVersion.cmake
    DESTINATION lib/cmake/DevToolsLog
)

#
# Finally export the Config which CMake will use
# when looking for matching libraries to link against.
#
install (
    FILES       DevToolsLogConfig.cmake
    DESTINATION lib/cmake/DevToolsLog
)
