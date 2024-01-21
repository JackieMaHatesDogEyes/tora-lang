cmake_minimum_required(VERSION 3.13)
project(tora)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_C_STANDARD 99)

include_directories(include)

set(TORA_CORE_FILES
    src/lapi.c
    src/lcode.c
    src/lctype.c
    src/ldebug.c
    src/ldo.c
    src/ldump.c
    src/lfunc.c
    src/lgc.c
    src/llex.c
    src/lmem.c
    src/lobject.c
    src/lopcodes.c
    src/lparser.c
    src/lstate.c
    src/lstring.c
    src/ltable.c
    src/ltm.c
    src/lundump.c
    src/lvm.c
    src/lzio.c
)

set(TORA_LIB_FILES
    src/lbaselib.c
    src/ldblib.c
    src/liolib.c
    src/lmathlib.c
    src/loslib.c
    src/ltablib.c
    src/lstrlib.c
    src/lutf8lib.c
    src/loadlib.c
    src/lcorolib.c
    src/linit.c
)

add_library(tora_core STATIC
    ${TORA_CORE_FILES}
)

add_library(tora_aux STATIC
    src/lauxlib.c
)

add_library(tora_libs STATIC
    ${TORA_LIB_FILES}
)


add_library(TORA_LIB SHARED ${TORA_CORE_FILES} ${TORA_LIB_FILES} src/lauxlib.c)
set_target_properties(TORA_LIB PROPERTIES OUTPUT_NAME "tora")

add_executable(tora src/tora.c)

target_link_libraries(tora tora_core tora_aux tora_libs)