# CMake版本信息
cmake_minimum_required(VERSION 3.4.1)

# 支持-std=gnu++11
set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

# 工程路径
set(pathToProject D:/android_studio_workspace/ARSimpleNativeCarsProj)
# Native 路径
set(pathToNative ${pathToProject}/aRSimpleNativeCars/src/main/cpp)

# 配置加载native依赖
include_directories(${pathToProject}/ARToolKit)

# 添加待编译的文件
add_library(ARWrapperNativeCarsExample SHARED ${pathToNative}/ARWrapperNativeCarsExample.cpp)

# 动态方式加载
add_library(so_libc++_shared SHARED IMPORTED)
# 引入so文件
set_target_properties(so_libc++_shared PROPERTIES IMPORTED_LOCATION ${pathToProject}/aRSimpleNativeCars/src/main/jniLibs/${ANDROID_ABI}/libc++_shared.so)

# 动态方式加载
add_library(so_libARWrapper SHARED IMPORTED)
# 引入so文件
set_target_properties(so_libARWrapper PROPERTIES IMPORTED_LOCATION ${pathToProject}/aRSimpleNativeCars/src/main/jniLibs/${ANDROID_ABI}/libARWrapper.so)

# 动态方式加载
add_library(so_libARWrapperNativeCarsExample SHARED IMPORTED)
# 引入so文件
set_target_properties(so_libARWrapperNativeCarsExample PROPERTIES IMPORTED_LOCATION ${pathToProject}/aRSimpleNativeCars/src/main/jniLibs/${ANDROID_ABI}/libARWrapperNativeCarsExample.so)

target_link_libraries(ARWrapperNativeCarsExample
                      so_libc++_shared so_libARWrapper so_libARWrapperNativeCarsExample
                      log GLESv1_CM)