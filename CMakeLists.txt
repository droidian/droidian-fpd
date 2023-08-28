cmake_minimum_required(VERSION 3.10)

project(droidian-fpd)

set(CMAKE_AUTOMOC ON)
find_package(Qt5DBus REQUIRED)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
link_libraries(hybris-common)

set(SOURCES
    src/droidian-fpd.cpp
    src/androidfp.cpp
    src/fpdcommunity.cpp
    src/hardware/biometry_fp_api.cpp
    src/util/property_store.cpp
)

set(HEADERS
    src/androidfp.h
    src/biometry.h
    src/fpdcommunity.h
    src/hardware/android_hw_module.h
    src/util/property_store.h
)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

target_link_libraries(${PROJECT_NAME} Qt5::DBus)

install(TARGETS ${PROJECT_NAME} DESTINATION /usr/bin/)
install(FILES org.droidian.fingerprint.conf DESTINATION /etc/dbus-1/system.d/)
