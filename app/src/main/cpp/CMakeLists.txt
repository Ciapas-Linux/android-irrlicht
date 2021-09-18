
cmake_minimum_required(VERSION 3.10.2)

# Declares and names the project.

project("irrlicht")

add_library( # Sets the name of the library.
        app-glue
        STATIC

        # Provides a relative path to your source file(s).
        # Associated headers in the same location as their source
        # file are automatically included.
        ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c )

add_library(lirrlicht STATIC IMPORTED)
set_target_properties(lirrlicht PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libIrrlicht.a)


add_library(native-lib SHARED

        main.cpp
        android_tools.cpp android_tools.h
         )

# Specifies a path to native header files.
include_directories(${CMAKE_CURRENT_SOURCE_DIR}
        ${ANDROID_NDK}/sources/android/native_app_glue/)
include_directories(/home/kot/irrlicht-ogles/include/)
#>>>    NOTE: The above should be YOUR Irrlicht include directory. This is mine.
#>>>          The path starts in the "app" directory of your project.

# Searches for a specified prebuilt library and stores the path as a
# variable. Because system libraries are included in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in the
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( native-lib
        app-glue
        android
        EGL
        log
        GLESv1_CM
        GLESv2
        z
        m
        ${log-lib}
        lirrlicht)







