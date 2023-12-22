cmake_minimum_required(VERSION 3.17)
project(ffmpeg_libav_tutorial)

find_package(PkgConfig REQUIRED)
pkg_check_modules(LIBAV REQUIRED IMPORTED_TARGET
    libavdevice
    libavfilter
    libavformat
    libavcodec
    libswresample
    libswscale
    libavutil
)

add_library(videodebugging video_debugging.c)
target_link_libraries(videodebugging
    PUBLIC
        PkgConfig::LIBAV
)

add_executable(hello 0_hello_world.c)
target_link_libraries(hello
    PRIVATE
    videodebugging
)

add_executable(remuxing 2_remuxing.c)
target_link_libraries(remuxing
    PRIVATE
    videodebugging
)

add_executable(transcoding 3_transcoding.c)
target_link_libraries(transcoding
    PRIVATE
    videodebugging
)
