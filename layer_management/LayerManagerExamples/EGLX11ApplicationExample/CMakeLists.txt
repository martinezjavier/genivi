############################################################################
# 
# Copyright 2010-2012 BMW Car IT GmbH 
# 
# 
# Licensed under the Apache License, Version 2.0 (the "License"); 
# you may not use this file except in compliance with the License. 
# You may obtain a copy of the License at 
#
#		http://www.apache.org/licenses/LICENSE-2.0 
#
# Unless required by applicable law or agreed to in writing, software 
# distributed under the License is distributed on an "AS IS" BASIS, 
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. 
# See the License for the specific language governing permissions and 
# limitations under the License.
#
############################################################################

cmake_minimum_required (VERSION 2.6)

project_type(EXAMPLE)

include_directories ("include")
include_directories ("../../LayerManagerClient/ilmClient/include")
include_directories ("../LayerSceneDescriptionExample/include")
include_directories ("../../LayerManagerUtils/include")

add_executable(EGLX11ApplicationExample src/egl_helper.cpp src/eglX11_application.cpp src/gles2application.cpp)

add_dependencies(EGLX11ApplicationExample ilmClient)
add_dependencies(EGLX11ApplicationExample LayerManagerUtils)

find_package (GLESv2 REQUIRED)
include_directories(${GLESv2_INCLUDE_DIR})

find_package (EGL REQUIRED)
include_directories(${EGL_INCLUDE_DIR})

find_package (X11 REQUIRED)
include_directories(${X11_INCLUDE_DIR})

set(LIBS ${LIBS} ${GLESv2_LIBRARIES} ${X11_LIBRARIES} ${EGL_LIBRARY} LayerManagerUtils) 
target_link_libraries(EGLX11ApplicationExample ${LIBS} ilmClient)

install (TARGETS EGLX11ApplicationExample DESTINATION bin)