# Copyright 2011,2012,2016,2018,2019 Free Software Foundation, Inc.
#
# This file was generated by gr_modtool, a tool from the GNU Radio framework
# This file is a part of gr-iqbal
#
# GNU Radio is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3, or (at your option)
# any later version.
#
# GNU Radio is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNU Radio; see the file COPYING.  If not, write to
# the Free Software Foundation, Inc., 51 Franklin Street,
# Boston, MA 02110-1301, USA.

########################################################################
# Setup library
########################################################################
include(GrPlatform) #define LIB_SUFFIX

list(APPEND iqbalance_sources
     fix_cc.cc
     optimize_c.cc
)

add_library(gnuradio-iqbalance SHARED ${iqbalance_sources} ${LIBOSMODSP_SEL_SOURCES})
target_link_libraries(gnuradio-iqbalance gnuradio::gnuradio-runtime ${LIBOSMODSP_SEL_LIBRARIES})
target_include_directories(gnuradio-iqbalance
    PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
    PUBLIC $<INSTALL_INTERFACE:include>
  )
set_target_properties(gnuradio-iqbalance PROPERTIES OUTPUT_NAME gnuradio-iqbalance)
set_target_properties(gnuradio-iqbalance PROPERTIES DEFINE_SYMBOL "gnuradio_iqbalance_EXPORTS")

if(APPLE)
    set_target_properties(gnuradio-iqbalance PROPERTIES
        INSTALL_NAME_DIR "${CMAKE_INSTALL_PREFIX}/lib"
    )
endif(APPLE)

########################################################################
# Install built library files
########################################################################
include(GrMiscUtils)
set(VERSION "3.8.0")
set(LIBVER "3.8.0")
GR_LIBRARY_FOO(gnuradio-iqbalance)

########################################################################
# Print summary
########################################################################
message(STATUS "Using install prefix: ${CMAKE_INSTALL_PREFIX}")
message(STATUS "Building for version: ${VERSION} / ${LIBVER}")

########################################################################
# Build and register unit test
########################################################################
find_package(Boost COMPONENTS unit_test_framework)

include(GrTest)
list(APPEND GR_TEST_TARGET_DEPS gnuradio-iqbalance)
#turn each test cpp file into an executable with an int main() function
add_definitions(-DBOOST_TEST_DYN_LINK -DBOOST_TEST_MAIN)
