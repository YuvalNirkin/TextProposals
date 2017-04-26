cmake_minimum_required(VERSION 2.8)
project(TextProposals)

# Set version
set(TEXT_PROPOSALS_MAJOR_VERSION 0)
set(TEXT_PROPOSALS_MINOR_VERSION 9)
set(TEXT_PROPOSALS_PATCH_VERSION 0)
set(TEXT_PROPOSALS_VERSION ${TEXT_PROPOSALS_MAJOR_VERSION}.${TEXT_PROPOSALS_MINOR_VERSION}.${TEXT_PROPOSALS_PATCH_VERSION})

# Global configurations
# ===================================================
if(WIN32)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DNOMINMAX -D_USE_MATH_DEFINES")
	set(DEF_INSTALL_CMAKE_DIR cmake)
else()
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -fPIC")
	set(DEF_INSTALL_CMAKE_DIR lib/cmake/${PROJECT_NAME})
endif()
set(INSTALL_CMAKE_DIR ${DEF_INSTALL_CMAKE_DIR} CACHE PATH
	"Installation directory for CMake files")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")
set(CMAKE_DEBUG_POSTFIX "_d" CACHE STRING
	"Add a custom \"postfix\" to static and shared libraries when in Debug build")
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# Optional 3rd party components
# ===================================================
option(WITH_BOOST_STATIC "Boost static libraries" ON)

# Build components
# ===================================================

# Find dependencies
# ===================================================

# Boost
set(Boost_USE_STATIC_LIBS ${WITH_BOOST_STATIC})
set(BOOST_ALL_DYN_LINK NOT ${WITH_BOOST_STATIC})
if(WIN32)
	if(${WITH_BOOST_STATIC})
		add_definitions(-DBOOST_ALL_NO_LIB)
	else()
		add_definitions(-DBOOST_ALL_DYN_LINK)
	endif()
endif()
find_package(Boost REQUIRED filesystem program_options regex timer)

# OpenCV
find_package(OpenCV REQUIRED highgui imgproc imgcodecs calib3d photo)

# Caffe
find_package(Caffe REQUIRED)

# glog
find_package(glog REQUIRED)

# protobuf
find_package(protobuf REQUIRED)

# Add sub-directories
# ===================================================
add_subdirectory(text_proposal)
add_subdirectory(img2hierarchy)
add_subdirectory(img2hierarchy_cnn)

# Export configuration
# ===================================================

# Install data
install(FILES trained_boost_groups.xml lex.txt
		DESTINATION bin)