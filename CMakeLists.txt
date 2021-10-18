cmake_minimum_required(VERSION 3.10)
project(libnih-dbus LANGUAGES C VERSION 1.0)

file(GLOB SRCS nih/*.c)
add_library(nih ${SRCS})
target_include_directories(nih PRIVATE ./)
file(GLOB HEADER nih/*.h)
set_target_properties(nih PROPERTIES PUBLIC_HEADER "${HEADER}")
install(TARGETS nih
    EXPORT ${CMAKE_PROJECT_NAME} DESTINATION lib
    PUBLIC_HEADER DESTINATION include/nih
)

file(GLOB SRCS nih-dbus/*.c)
add_library(nih-dbus ${SRCS})
target_include_directories(nih-dbus PRIVATE ./)
file(GLOB HEADER nih-dbus/*.h)
set_target_properties(nih-dbus PROPERTIES PUBLIC_HEADER "${HEADER}")
install(TARGETS nih-dbus 
    EXPORT ${CMAKE_PROJECT_NAME} DESTINATION lib
    PUBLIC_HEADER DESTINATION include/nih-dbus
)

install(DIRECTORY dbus/ DESTINATION include/dbus)
