# Copyright (c) 2018 Cisco and/or its affiliates.
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at:
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

##############################################################################
# Generate vlib/config.h
##############################################################################
set(PRE_DATA_SIZE 128 CACHE STRING "Buffer headroom size.")
configure_file(
  ${CMAKE_SOURCE_DIR}/vlib/config.h.in
  ${CMAKE_BINARY_DIR}/vlib/config.h
)
install(
  FILES ${CMAKE_BINARY_DIR}/vlib/config.h
  DESTINATION include/vlib
  COMPONENT vpp-dev
)

##############################################################################
# vlib shared library
##############################################################################
add_vpp_library(vlib
  SOURCES
  buffer.c
  buffer_serialize.c
  cli.c
  counter.c
  error.c
  format.c
  i2c.c
  init.c
  linux/pci.c
  linux/physmem.c
  linux/vfio.c
  log.c
  main.c
  node.c
  node_cli.c
  node_format.c
  pci/pci.c
  threads.c
  threads_cli.c
  trace.c
  unix/cj.c
  unix/cli.c
  unix/input.c
  unix/main.c
  unix/plugin.c
  unix/util.c

  INSTALL_HEADERS
  buffer_funcs.h
  buffer.h
  buffer_node.h
  cli_funcs.h
  cli.h
  counter.h
  counter_types.h
  defs.h
  error_funcs.h
  error.h
  format_funcs.h
  global_funcs.h
  i2c.h
  init.h
  linux/vfio.h
  log.h
  main.h
  node_funcs.h
  node.h
  pci/pci_config.h
  pci/pci.h
  physmem_funcs.h
  physmem.h
  threads.h
  trace_funcs.h
  trace.h
  unix/cj.h
  unix/mc_socket.h
  unix/plugin.h
  unix/unix.h
  vlib.h

  LINK_LIBRARIES vppinfra svm ${CMAKE_DL_LIBS}
)
