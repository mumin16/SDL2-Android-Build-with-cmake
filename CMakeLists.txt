cmake_minimum_required(VERSION 3.0.0)

set(SDL_DIR "/home/x64/Desktop/SDL-2.23.0-fd2a2ee")
set(ANDROID_NDK "/home/x64/Desktop/android-ndk-r25-beta4")
set(ANDROID_ABI "x86_64") #arm64-v8a , x86 ,armeabi-v7a
set(ANDROID_PLATFORM "android-26")#27 28 .. 32 

set(CMAKE_TOOLCHAIN_FILE "${ANDROID_NDK}/build/cmake/android.toolchain.cmake")
set(CMAKE_ANDROID_ARCH_ABI "${ANDROID_ABI}")
set(CMAKE_ANDROID_NDK "${ANDROID_NDK}")
set(CMAKE_SYSTEM_NAME "Android")
set(CMAKE_SYSTEM_VERSION "26")
#set(CMAKE_MAKE_PROGRAM "/home/x64/Android/Sdk/cmake/3.18.1/bin/ninja")

add_compile_definitions(GL_GLEXT_PROTOTYPES)

set(LIBRARY_OUTPUT_PATH "./${ANDROID_ABI}")

project(SDL_BUILD VERSION 0.1.0)

include_directories(${SDL_DIR}/include)
file(GLOB SRC_FILES ${SDL_DIR}/src/*.c
${SDL_DIR}/src/audio/*.c
${SDL_DIR}/src/audio/android/*.c
${SDL_DIR}/src/audio/dummy/*.c
${SDL_DIR}/src/audio/aaudio/*.c
${SDL_DIR}/src/audio/openslES/*.c
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
${SDL_DIR}/src/sensor/*.c
${SDL_DIR}/src/sensor/android/*.c
${SDL_DIR}/src/render/*.c
${SDL_DIR}/src/render/*/*.c
${SDL_DIR}/src/stdlib/*.c
${SDL_DIR}/src/thread/*.c
${SDL_DIR}/src/thread/pthread/*.c
${SDL_DIR}/src/timer/*.c
${SDL_DIR}/src/timer/unix/*.c
${SDL_DIR}/src/video/*.c
${SDL_DIR}/src/video/android/*.c
${SDL_DIR}/src/video/yuv2rgb/*.c
${SDL_DIR}/src/test/*.c)

add_library(SDL2_static STATIC ${SRC_FILES})
add_library(SDL2 SHARED ${SRC_FILES})
target_link_libraries(SDL2 dl GLESv1_CM GLESv2 OpenSLES log android)
