cmake_minimum_required(VERSION 3.13)

add_library(Rp2xxx_rtc INTERFACE)
target_include_directories(Rp2xxx_rtc INTERFACE
 ${CMAKE_CURRENT_LIST_DIR}
)
target_link_libraries(Rp2xxx_rtc INTERFACE pico_stdlib)
target_sources(Rp2xxx_rtc INTERFACE
    ${CMAKE_CURRENT_LIST_DIR}/rp2xxx_rtc.cpp
)

if(${PICO_PLATFORM} MATCHES "rp2040")
target_link_libraries(Rp2xxx_rtc INTERFACE hardware_rtc)
target_sources(Rp2xxx_rtc INTERFACE
    ${CMAKE_CURRENT_LIST_DIR}/rp2040_rtc.cpp
)
else()
target_sources(Rp2xxx_rtc INTERFACE
    ${CMAKE_CURRENT_LIST_DIR}/rp2350_rtc.cpp
)
target_link_libraries(Rp2xxx_rtc INTERFACE pico_aon_timer)
endif()
