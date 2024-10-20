cmake_minimum_required(VERSION 2.4)
if(COMMAND cmake_policy)
    cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

project(buildroot)

if(CMAKE_SYSTEM_NAME MATCHES "Darwin")
   MESSAGE("Compiling for MacOS/Darwin")
   # set(CMAKE_C_COMPILER /opt/homebrew/bin/gcc-14)
   # set(CMAKE_CXX_COMPILER /opt/homebrew/bin/g++-14)
   set(COINUTILS_INCLUDES /opt/homebrew/opt/coinutils/include/coinutils)
   # set(COINUTILS_LIBRARIES /opt/homebrew/opt/coinutils/lib)
   set(CBC_INCLUDES /opt/homebrew/opt/cbc/include/cbc)
   # set(CBC_LIBRARIES /opt/homebrew/opt/cbc/lib)
   set(CGL_INCLUDES /opt/homebrew/opt/cgl/include/cgl)
   # set(CGL_LIBRARIES /opt/homebrew/opt/cgl/lib)
   set(OSI_INCLUDES /opt/homebrew/opt/osi/include/osi)
   # set(OSI_LIBRARIES /opt/homebrew/opt/osi/lib)
   set(CLP_INCLUDES /opt/homebrew/opt/clp/include/clp)
   # set(CLP_LIBRARIES /opt/homebrew/opt/clp/lib)
   # set(GSL_INCLUDES /opt/homebrew/opt/gsl/include)
   # set(GSL_LIBRARIES /opt/homebrew/opt/gsl/lib)


   set(DOXYFILE_IN ${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in)

   set(CMAKE_CXX_FLAGS "--std=gnu++11 -I/Library/Developer/CommandLineTools/usr/include -g3 -O -fprofile-arcs -Wno-conversion-null -Wno-enum-compare -Wno-maybe-uninitialized -Wno-switch -Wno-nonnull-compare -Wno-unused-but-set-variable -Wno-unused-variable -Wno-sign-compare")

   set(CMAKE_CXX_LINK_FLAGS "-L/opt/homebrew/opt/flex/lib")

ELSE()

  MESSAGE("Compiling assuming Linux environment")
  set(CMAKE_CXX_FLAGS "-g3 -O -fprofile-arcs -Wno-conversion-null -Wno-enum-compare -Wno-maybe-uninitialized -Wno-switch -Wno-nonnull-compare -Wno-unused-but-set-variable -Wno-unused-variable -Wno-sign-compare")

ENDIF()


set(CMAKE_CXX_FLAGS_PROFILE "-g3 -pg -O -fprofile-arcs -Wno-unused-but-set-variable -Wno-unused-variable -Wno-sign-compare")

set(CMAKE_CXX_LINK_FLAGS_PROFILE "-pg")

add_subdirectory(VALfiles)


if(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/optic")
	add_subdirectory(optic)
endif(EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/optic")
