#
# Project Definition
#
cmake_minimum_required(VERSION 3.8.2)
project(DevToolsLog)

#
# Exported Library
#
add_library(Log STATIC src/logger.cpp include/logger.h include/logger_preProcessor.h)
target_include_directories(Log PUBLIC include)
