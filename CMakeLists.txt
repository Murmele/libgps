cmake_minimum_required(VERSION 2.6)
set(PROJECT_NAME position_logger)
project(${PROJECT_NAME})

add_library(gps STATIC "")
target_link_libraries(gps m)
target_include_directories(gps PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)

target_sources(gps PUBLIC 
               ${CMAKE_CURRENT_SOURCE_DIR}/src/gps.h
               ${CMAKE_CURRENT_SOURCE_DIR}/src/nmea.h
               ${CMAKE_CURRENT_SOURCE_DIR}/src/serial.h)

target_sources(gps PRIVATE 
               ${CMAKE_CURRENT_SOURCE_DIR}/src/gps.c
               ${CMAKE_CURRENT_SOURCE_DIR}/src/nmea.c
               ${CMAKE_CURRENT_SOURCE_DIR}/src/serial.c)

add_executable(${PROJECT_NAME} examples/position_logger.c)
target_link_libraries(${PROJECT_NAME} gps)

install(TARGETS gps DESTINATION /usr/local/lib)
install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
