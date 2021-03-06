# This source file is part of the Swift.org open source project
#
# Copyright (c) 2014 - 2020 Apple Inc. and the Swift project authors
# Licensed under Apache License v2.0 with Runtime Library Exception
#
# See http://swift.org/LICENSE.txt for license information
# See http://swift.org/CONTRIBUTORS.txt for Swift project authors

add_library(TSCLibc
  libc.swift)

if(CMAKE_SYSTEM_NAME STREQUAL Windows)
  target_compile_options(TSCLibc PRIVATE
    -autolink-force-load)
endif()
# NOTE(compnerd) workaround for CMake not setting up include flags yet
set_target_properties(TSCLibc PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_Swift_MODULE_DIRECTORY})


if(CMAKE_SYSTEM_NAME STREQUAL Windows)
install(TARGETS TSCLibc
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin)
endif()

set_property(GLOBAL APPEND PROPERTY TSC_EXPORTS TSCLibc)
