cmake_minimum_required(VERSION 3.11)

project(nbperf C)

set(SRCS
  nbperf.c
  nbperf-bdz.c
  nbperf-chm.c
  nbperf-chm3.c
  graph2.c
  graph3.c)

set(HEADERS
  mi_vector_hash.h
  mi_wyhash.h
  wyhash.h
  fnv3.h
  crc3.h)

find_package(Git REQUIRED)

# Get short hash from Git
execute_process(
  COMMAND ${GIT_EXECUTABLE} log -1 --format=%h
  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
  OUTPUT_VARIABLE VERSION
  OUTPUT_STRIP_TRAILING_WHITESPACE
  )

add_executable(nbperf ${SRCS} mi_vector_hash.c)
target_compile_definitions(nbperf PUBLIC
  VERSION="${VERSION}"
  HAVE_NBTOOL_CONFIG_H)
target_link_libraries(nbperf m)
