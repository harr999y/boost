##########################################################################
# Copyright (C) 2007-2009 Douglas Gregor <doug.gregor@gmail.com>         #
# Copyright (C) 2007-2009 Troy Straszheim <troy@resophonic.com>          #
# Copyright (C) 2010-2011 Daniel Pfeifer <daniel@pfeifer-mail.de>        #
#                                                                        #
# Distributed under the Boost Software License, Version 1.0.             #
# See accompanying file LICENSE_1_0.txt or copy at                       #
#   http://www.boost.org/LICENSE_1_0.txt                                 #
##########################################################################

cmake_minimum_required(VERSION 2.8.4 FATAL_ERROR)
project(Boost)

##########################################################################
# Config Information                                                     #
##########################################################################

set(BOOST_CONFIG_VERSION "1.47")

file(WRITE "${PROJECT_BINARY_DIR}/boost-config-version.cmake"
  "set(PACKAGE_VERSION \"${BOOST_CONFIG_VERSION}\")\n"
  "set(PACKAGE_VERSION_EXACT TRUE)\n"
  )

file(WRITE "${Boost_BINARY_DIR}/boost-config.cmake"
  "set(Boost_FOUND TRUE)\n"
  "set(Boost_INCLUDE_DIRS \"${Boost_BINARY_DIR}/include\")\n"
  "set(Boost_LIBRARY_DIRS \"${Boost_BINARY_DIR}/lib\")\n"
  "set(Boost_RESOURCE_PATH \"${Boost_SOURCE_DIR}/tools/cmake/resources\")\n"
  "set(BOOSTBOOK_CATALOG \"${Boost_BINARY_DIR}/tools/boostbook/catalog.xml\")\n"
  "set(BOOSTBOOK_XSL_DIR \"${Boost_SOURCE_DIR}/tools/boostbook/xsl\")\n"
  "set(Boost_USE_FILE \"${Boost_SOURCE_DIR}/tools/cmake/modules/UseBoost.cmake\")\n"
  "set(Boost_DEV_FILE \"${Boost_SOURCE_DIR}/tools/cmake/modules/UseBoostDev.cmake\")\n"
  )

set(Boost_DIR "${Boost_BINARY_DIR}")
find_package(Boost NO_MODULE)
include("${Boost_DEV_FILE}")

option(BOOST_DEBIAN_PACKAGES "Create debian packages" OFF)

##########################################################################
# Building and Testing                                                   #
##########################################################################

set(BOOST_ENABLED_DOCS "ALL"
  CACHE STRING "valid values are ALL, NONE, or a ; separated list of components"
  )
set(BOOST_ENABLED_TESTS "ALL"
  CACHE STRING "valid values are ALL, NONE, or a ; separated list of components"
  )
set(BOOST_ENABLED_EXAMPLES "NONE"
  CACHE STRING "valid values are ALL, NONE, or a ; separated list of components"
  )

# As long as CTest does not support incremental testing, we disable the
# builtin test target and create our own. This target should be "built"
# with the "keep going" option, eg: 'make test -k'.
add_custom_target(test)
#enable_testing()

# make visual studio look nice
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Put the libaries and binaries that get built into directories at the
# top of the build tree rather than in hard-to-find leaf
# directories. This simplifies manual testing and the use of the build
# tree rather than installed Boost libraries.
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)

##########################################################################
# Components                                                             #
##########################################################################

set(BOOST_PROJECTS_ALL)
add_subdirectory(libs/accumulators)
add_subdirectory(libs/algorithm)
add_subdirectory(libs/any)
add_subdirectory(libs/array)
add_subdirectory(libs/asio)
add_subdirectory(libs/assign)
add_subdirectory(libs/bimap)
add_subdirectory(libs/bind)
add_subdirectory(libs/chrono)
add_subdirectory(libs/circular_buffer)
add_subdirectory(libs/compatibility)
add_subdirectory(libs/concept_check)
add_subdirectory(libs/config)
add_subdirectory(libs/conversion)
add_subdirectory(libs/core)
add_subdirectory(libs/crc)
add_subdirectory(libs/date_time)
add_subdirectory(libs/detail)
add_subdirectory(libs/disjoint_sets)
add_subdirectory(libs/dynamic_bitset)
add_subdirectory(libs/exception)
add_subdirectory(libs/filesystem)
add_subdirectory(libs/flyweight)
add_subdirectory(libs/foreach)
add_subdirectory(libs/format)
add_subdirectory(libs/function)
add_subdirectory(libs/function_types)
add_subdirectory(libs/functional)
add_subdirectory(libs/fusion)
add_subdirectory(libs/geometry)
add_subdirectory(libs/gil)
add_subdirectory(libs/graph)
add_subdirectory(libs/graph_parallel)
add_subdirectory(libs/icl)
add_subdirectory(libs/integer)
add_subdirectory(libs/interprocess)
add_subdirectory(libs/intrusive)
add_subdirectory(libs/io)
add_subdirectory(libs/iostreams)
add_subdirectory(libs/iterator)
add_subdirectory(libs/lambda)
add_subdirectory(libs/logic)
add_subdirectory(libs/math)
add_subdirectory(libs/move)
add_subdirectory(libs/mpi)
add_subdirectory(libs/mpl)
add_subdirectory(libs/msm)
add_subdirectory(libs/multi_array)
add_subdirectory(libs/multi_index)
add_subdirectory(libs/numeric)
add_subdirectory(libs/optional)
add_subdirectory(libs/parameter)
add_subdirectory(libs/phoenix)
add_subdirectory(libs/polygon)
add_subdirectory(libs/pool)
add_subdirectory(libs/preprocessor)
add_subdirectory(libs/program_options)
add_subdirectory(libs/property_map)
add_subdirectory(libs/property_tree)
add_subdirectory(libs/proto)
add_subdirectory(libs/ptr_container)
add_subdirectory(libs/python)
add_subdirectory(libs/random)
add_subdirectory(libs/range)
add_subdirectory(libs/ratio)
add_subdirectory(libs/rational)
add_subdirectory(libs/regex)
add_subdirectory(libs/scope_exit)
add_subdirectory(libs/serialization)
add_subdirectory(libs/signals)
add_subdirectory(libs/signals2)
add_subdirectory(libs/smart_ptr)
add_subdirectory(libs/spirit)
add_subdirectory(libs/statechart)
add_subdirectory(libs/static_assert)
add_subdirectory(libs/system)
add_subdirectory(libs/test)
add_subdirectory(libs/thread)
add_subdirectory(libs/timer)
add_subdirectory(libs/tokenizer)
add_subdirectory(libs/tr1)
add_subdirectory(libs/tuple)
add_subdirectory(libs/type_traits)
add_subdirectory(libs/typeof)
add_subdirectory(libs/units)
add_subdirectory(libs/unordered)
add_subdirectory(libs/utility)
add_subdirectory(libs/uuid)
add_subdirectory(libs/variant)
add_subdirectory(libs/wave)
add_subdirectory(libs/xpressive)
add_subdirectory(tools/auto_index)
add_subdirectory(tools/bcp)
add_subdirectory(tools/boostbook)
add_subdirectory(tools/build)
add_subdirectory(tools/inspect)
add_subdirectory(tools/litre)
add_subdirectory(tools/quickbook)
add_subdirectory(tools/cmake)

##########################################################################
# Package Information                                                    #
##########################################################################

set(CPACK_PACKAGE_NAME "Boost")
set(CPACK_PACKAGE_VENDOR "http://www.boost.org")
set(CPACK_PACKAGE_CONTACT "Daniel Pfeifer <daniel@pfeifer-mail.de>")
set(CPACK_PACKAGE_VERSION "${Boost_VERSION}")
set(CPACK_PACKAGE_FILE_NAME "Boost-${Boost_VERSION}-${CMAKE_SYSTEM_NAME}-${BOOST_TOOLSET}")
set(CPACK_SOURCE_IGNORE_FILES "${Boost_BINARY_DIR}/;/\\\\.git")

include(BoostCPack)
