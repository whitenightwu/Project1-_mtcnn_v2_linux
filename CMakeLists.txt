#1.cmake verson，指定cmake的最小版本号 
# cmake_minimum_required(VERSION 2.8)
# cmake_minimum_required(VERSION 3.11)
cmake_minimum_required(VERSION 3.5)

#2.project name，指定项目的名称，一般和项目的文件夹名称对应
project(mtcnn_ncnn C CXX)

#3.set environment variable，设置环境变量
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

#4.include头文件目录 
include_directories(${CMAKE_CURRENT_LIST_DIR}/3rdparty/include/include
					${CMAKE_CURRENT_LIST_DIR}/3rdparty/include/include/opencv
					${CMAKE_CURRENT_LIST_DIR}/3rdparty/include/include/opencv2
					${CMAKE_CURRENT_LIST_DIR}/3rdparty/include/ncnn
                    ${CMAKE_CURRENT_LIST_DIR}/src)

#5.library目录及name名称
link_directories(${CMAKE_CURRENT_LIST_DIR}/3rdparty/lib)

# list(APPEND MTCNN_LINKER_LIBS opencv_world ippicv opencv_line_descriptor libjasper opencv_optflow libjpeg	 opencv_phase_unwrapping libpng opencv_plot libprotobuf opencv_reg libtiff opencv_rgbd ncnn opencv_saliency opencv_aruco opencv_stereo opencv_bgsegm opencv_structured_light opencv_bioinspired  opencv_surface_matching opencv_ccalib opencv_text opencv_dnn opencv_tracking opencv_dpm  opencv_face opencv_ximgproc opencv_freetype zlib opencv_fuzzy)

######

# list(APPEND MTCNN_LINKER_LIBS opencv_plot opencv_world ncnn  pthread libprotobuf  zlib libtiff libpng libjpeg png z jasper jpeg ippicv dc1394 avcodec-ffmpeg avformat-ffmpeg avutil-ffmpeg swscale-ffmpeg gphoto2 gphoto2_port  exif dl m  rt)

######

# list(APPEND MTCNN_LINKER_LIBS opencv_world ncnn ippicv zlib libtiff libpng libjpeg png z jasper jpeg pthread libprotobuf IlmImf dc1394 avcodec-ffmpeg avformat-ffmpeg avutil-ffmpeg swscale-ffmpeg gphoto2 gphoto2_port exif dl m  rt tbb libjasper)

#######  1)
list(APPEND MTCNN_LINKER_LIBS zlib opencv_world ncnn ippicv zlib libtiff libpng libjpeg png z jasper jpeg pthread dc1394 avcodec-ffmpeg avformat-ffmpeg avutil-ffmpeg swscale-ffmpeg gphoto2 gphoto2_port exif dl m  rt libprotobuf Half IlmImf IlmThread )

# avutil
# Qt5Core Qt5Gui Qt5Widgets
# Imath Iex Half IlmThread IlmImf
# gtk+-2.0
# Imath IlmImf Iex Half IlmThread
# libprotobuf
# cocos2dx_static libtegra_hal
# 
# libwebp


#6.source directory源文件目录
file(GLOB MTCNN_SRC ${CMAKE_CURRENT_LIST_DIR}/src/*.h
                    ${CMAKE_CURRENT_LIST_DIR}/src/*.cpp)
set(MTCNN_COMPILE_CODE ${MTCNN_SRC})

#7.1.add executable file，编译为可执行文件
# add_executable(mtcnn_ncnn ${MTCNN_COMPILE_CODE})
#7.2.add library file，编译为动态库
add_library(mtcnn_ncnn SHARED ${MTCNN_COMPILE_CODE})

#8.add link library，添加工程所依赖的库
target_link_libraries(mtcnn_ncnn ${MTCNN_LINKER_LIBS})
