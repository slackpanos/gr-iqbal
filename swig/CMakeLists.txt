# Copyright 2011 Free Software Foundation, Inc.
#
# This file is part of GNU Radio
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
# Include swig generation macros
########################################################################
find_package(SWIG)
find_package(PythonLibs 3)
if(NOT SWIG_FOUND OR NOT PYTHONLIBS_FOUND)
    return()
endif()
include(GrSwig)
include(GrPython)

########################################################################
# Setup swig generation
########################################################################
set(GR_SWIG_INCLUDE_DIRS $<TARGET_PROPERTY:gnuradio::runtime_swig,INTERFACE_INCLUDE_DIRECTORIES>)
set(GR_SWIG_TARGET_DEPS gnuradio::runtime_swig)

set(GR_SWIG_LIBRARIES gnuradio-iqbalance)

set(GR_SWIG_DOC_FILE ${CMAKE_CURRENT_BINARY_DIR}/iqbalance_swig_doc.i)
set(GR_SWIG_DOC_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/../include/gnuradio/iqbalance)
set(GR_SWIG_DOCS_TARGET_DEPS runtime_swig_swig_doc)

GR_SWIG_MAKE(iqbalance_swig iqbalance_swig.i)

########################################################################
# Install the build swig module
########################################################################
GR_SWIG_INSTALL(TARGETS iqbalance_swig DESTINATION ${GR_PYTHON_DIR}/gnuradio/iqbalance)

########################################################################
# Install swig .i files for development
########################################################################
install(
    FILES
    iqbalance_swig.i
    ${CMAKE_CURRENT_BINARY_DIR}/iqbalance_swig_doc.i
    DESTINATION ${GR_INCLUDE_DIR}/gnuradio/swig
)
