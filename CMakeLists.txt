project( boostfuture )
cmake_minimum_required( VERSION 2.6 )

# set cxx flag
if (${CMAKE_CXX_COMPILER_ID} MATCHES GNU)
  set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++11")
elseif (${CMAKE_CXX_COMPILER_ID} MATCHES Clang)
  if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    # We want to link in C++11 mode if we're using Clang and on OS X.
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -ftemplate-depth=256 -std=c++11 -stdlib=libc++")
  else()
    # We just add the -Wall and a high enough template depth
    # flag for Clang in other systems.
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -ftemplate-dempth=256")
  endif()
endif()

find_package( Boost  1.63.0  COMPONENTS thread system chrono REQUIRED)
include_directories( ${Boost_INCLUDE_DIR} )
link_directories( ${Boost_LIBRARY_DIRS} )
set( Boost_USE_STATIC_LIBS        ON)
#set( Boost_USE_MULTITHREADED      ON )
#set( Boost_USE_STATIC_RUNTIME     OFF )
#set( BOOST_ALL_DYN_LINK           ON )

add_executable( ${PROJECT_NAME} main.cpp )
target_link_libraries( ${PROJECT_NAME} ${Boost_LIBRARIES} )

