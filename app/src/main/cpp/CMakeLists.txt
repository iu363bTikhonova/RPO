# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html.
# For more examples on how to use CMake, see https://github.com/android/ndk-samples.

# Sets the minimum CMake version required for this project.
cmake_minimum_required(VERSION 3.22.1)

# Declares the project name. The project name can be accessed via ${ PROJECT_NAME},
# Since this is the top level CMakeLists.txt, the project name is also accessible
# with ${CMAKE_PROJECT_NAME} (both CMake variables are in-sync within the top level
# build script scope).
project("fclient")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.
#
# In this top level CMakeLists.txt, ${CMAKE_PROJECT_NAME} is used to define
# the target library name; in the sub-module's CMakeLists.txt, ${PROJECT_NAME}
# is preferred for the same purpose.
#
# In order to load a library into your app from Java/Kotlin, you must call
# System.loadLibrary() and pass the name of the library defined here;
# for GameActivity/NativeActivity derived applications, the same library name must be
# used in the AndroidManifest.xml file.


add_library(spdlog STATIC IMPORTED)
add_library(mbedcrypto SHARED IMPORTED)
set_target_properties(spdlog PROPERTIES IMPORTED_LOCATION
        /home/user_1/AndroidStudioProjects/libs/spdlog/build/${ANDROID_ABI}/libspdlog.a)
set_target_properties(mbedcrypto PROPERTIES IMPORTED_LOCATION
        /home/user_1/AndroidStudioProjects/libs/mbedtls/build/x86_64/library/libmbedcrypto.so)
target_include_directories(spdlog INTERFACE
        /home/user_1/AndroidStudioProjects/libs/spdlog/spdlog/include
        /home/user_1/AndroidStudioProjects/libs/mbedtls/mbedtls/include/

)



add_library(${CMAKE_PROJECT_NAME} SHARED
        native-lib.cpp)

target_link_libraries(${CMAKE_PROJECT_NAME}
        spdlog
        android
        mbedcrypto
        log)