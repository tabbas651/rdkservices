# If not stated otherwise in this file or this component's LICENSE file the
# following copyright and licenses apply:
#
# Copyright 2020 RDK Management
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

option(PLUGIN_WEBKITBROWSER_TESTING_USE_WESTEROS "Enable westeros simpleshell protocol for input focus stacking" OFF)

target_include_directories(${PLUGIN_WEBKITBROWSER_IMPLEMENTATION} PRIVATE Testing)
target_sources(${PLUGIN_WEBKITBROWSER_IMPLEMENTATION} PRIVATE
    Testing/testrunner.cpp
)

if (PLUGIN_WEBKITBROWSER_TESTING_USE_WESTEROS)
    target_sources(${PLUGIN_WEBKITBROWSER_IMPLEMENTATION} PRIVATE Testing/westerosfocusmanager.cpp)
    target_link_libraries(${PLUGIN_WEBKITBROWSER_IMPLEMENTATION} PRIVATE
        wayland-client
        westeros_simpleshell_client
    )
else()
    target_sources(${PLUGIN_WEBKITBROWSER_IMPLEMENTATION} PRIVATE Testing/mockfocusmanager.cpp)
endif()

