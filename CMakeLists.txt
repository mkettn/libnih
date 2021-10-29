cmake_minimum_required(VERSION 3.10)

project(nih VERSION 1.0 LANGUAGES C)

#find_package(EXPAT 2.4.1 REQUIRED)
find_package(EXPAT)
find_package(DBus1)

option(LIBNIH_HOST_ARCH:STRING "target architecture for libnih to run on" arm-linux-musleabihf)

include(ExternalProject)
find_program(MAKE_EXE NAMES gmake nmake make)
# TODO use variable instead of constant absolute path
ExternalProject_Add(libnih-dbus
  SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}
  CONFIGURE_COMMAND autoreconf -fi
  BUILD_COMMAND ${CMAKE_CURRENT_SOURCE_DIR}/configure --host=${LIBNIH_HOST_ARCH} --disable-shared "CFLAGS=${CMAKE_C_FLAGS} -I${EXPAT_INCLUDE_DIRS} -I${DBus1_INCLUDE_DIR}" "CC=${CMAKE_C_COMPILER}" "LDFLAGS=-L/home/markk/4diac-forte/cget/hrs/lib" NIH_DBUS_TOOL=${NIH_DBUS_TOOL}
  COMMAND ${MAKE_EXE}
  INSTALL_COMMAND ${MAKE_EXE} install
  DEPENDS EXPAT::EXPAT
  BUILD_IN_SOURCE 1
  )
# TODO build libnih dbus tool if required
