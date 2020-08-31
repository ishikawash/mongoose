cmake_minimum_required(VERSION 3.16.0)
project(mongoose VERSION 0.1.0)

add_definitions(
    -DMG_ENABLE_HTTP_STREAMING_MULTIPART=1
    -DMG_ENABLE_HTTP_WEBDAV=1
    -DMG_ENABLE_FAKE_DAVLOCK=1
    -DMG_DISABLE_DAV_AUTH
)

add_library(mongoose mongoose.c mongoose.h)
target_compile_options(mongoose PRIVATE -g -Wall -Wno-unused-function)

add_executable(simplest_web_server ${CMAKE_CURRENT_LIST_DIR}/examples/simplest_web_server/simplest_web_server.c)
target_compile_options(simplest_web_server PRIVATE -g -Wall -Wno-unused-function)
target_include_directories(simplest_web_server PUBLIC ${CMAKE_CURRENT_LIST_DIR})
target_link_libraries(simplest_web_server mongoose pthread)
