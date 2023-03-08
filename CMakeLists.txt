cmake_minimum_required(VERSION 3.0.0)

if (NOT EXISTS ${CMAKE_BINARY_DIR}/CMakeCache.txt)
  if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "" FORCE)
  endif()
endif()

set(SDL_DIR "/home/x64/Downloads/SDL2-2.26.4")
set(ANDROID_NDK "/home/x64/Android/Sdk/ndk/25.2.9519653")
set(ANDROID_ABI "arm64-v8a") #arm64-v8a ,x86, x86_64 ,armeabi-v7a
set(ANDROID_PLATFORM "android-26")#27 28 .. 32 

set(CMAKE_TOOLCHAIN_FILE "${ANDROID_NDK}/build/cmake/android.toolchain.cmake")
set(CMAKE_ANDROID_ARCH_ABI "${ANDROID_ABI}")
set(CMAKE_ANDROID_NDK "${ANDROID_NDK}")
set(CMAKE_SYSTEM_NAME "Android")
set(CMAKE_SYSTEM_VERSION "26")
#set(CMAKE_MAKE_PROGRAM "/home/x64/Android/Sdk/cmake/3.22.1/bin/ninja")

add_compile_definitions(GL_GLEXT_PROTOTYPES)
add_compile_definitions(SDL_AUDIO_DISABLED)
add_compile_definitions(SDL_SENSOR_DISABLED)
add_compile_definitions(SDL_RENDER_DISABLED)


set(LIBRARY_OUTPUT_PATH "./${ANDROID_ABI}")

project(SDL_BUILD VERSION 0.1.0)

include_directories(${SDL_DIR}/include)
file(GLOB SRC_FILES ${SDL_DIR}/src/*.c
${SDL_DIR}/src/atomic/SDL_atomic.c
${SDL_DIR}/src/atomic/SDL_spinlock.c
${SDL_DIR}/src/core/android/*.c
${SDL_DIR}/src/cpuinfo/*.c
${SDL_DIR}/src/dynapi/*.c
${SDL_DIR}/src/events/*.c
${SDL_DIR}/src/file/*.c
${SDL_DIR}/src/haptic/*.c
${SDL_DIR}/src/haptic/android/*.c
${SDL_DIR}/src/hidapi/*.c
${SDL_DIR}/src/hidapi/android/*.cpp
${SDL_DIR}/src/joystick/*.c
${SDL_DIR}/src/joystick/android/*.c
${SDL_DIR}/src/joystick/hidapi/*.c
${SDL_DIR}/src/joystick/virtual/*.c
${SDL_DIR}/src/loadso/dlopen/*.c
${SDL_DIR}/src/locale/*.c
${SDL_DIR}/src/locale/android/*.c
${SDL_DIR}/src/misc/*.c
${SDL_DIR}/src/misc/android/*.c
${SDL_DIR}/src/power/*.c
${SDL_DIR}/src/power/android/*.c
${SDL_DIR}/src/filesystem/android/*.c
${SDL_DIR}/src/render/*.c
${SDL_DIR}/src/render/*/*.c
${SDL_DIR}/src/stdlib/*.c
${SDL_DIR}/src/thread/*.c
${SDL_DIR}/src/thread/pthread/*.c
${SDL_DIR}/src/timer/*.c
${SDL_DIR}/src/timer/unix/*.c
${SDL_DIR}/src/video/*.c
${SDL_DIR}/src/video/android/*.c
${SDL_DIR}/src/video/yuv2rgb/*.c)

add_library(SDL2_static STATIC ${SRC_FILES})
add_library(SDL2 SHARED ${SRC_FILES})
target_link_libraries(SDL2 dl GLESv1_CM GLESv2 log android)
