cmake_minimum_required(VERSION 3.10)

project(nih-dbus VERSION 1.0 LANGUAGES C)

file(GLOB SRCS nih/*.c)

add_library(nih
  ${SRCS}
  )

target_include_directories(nih PRIVATE
  ./
  )

file(GLOB SRCS nih-dbus/*.c)
add_library(nih-dbus
  ${SRCS})

target_include_directories(nih-dbus PRIVATE
  ./
  )

target_include_directories(nih-dbus SYSTEM PRIVATE
  ./
  )

target_link_libraries(nih-dbus libnih)

