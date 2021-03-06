    cmake_minimum_required(VERSION 3.4)

    set(CMAKE_CXX_STANDARD 11)
    set(CMAKE_CXX_STANDARD_REQUIRED ON)

    option(BUILD_EXAMPLES "Build examples" OFF)

    project(print)

    add_library(print STATIC /sources/print.cpp)

    target_include_directories(print PUBLIC
    $<BUILD_INTERFACE:/include>
    $<INSTALL_INTERFACE:include>
    )

    if(BUILD_EXAMPLES)
    file(GLOB EXAMPLE_SOURCES "/examples/*.cpp")
    foreach(EXAMPLE_SOURCE )
    get_filename_component(EXAMPLE_NAME  NAME_WE)
    add_executable( )
    target_link_libraries( print)
    install(TARGETS 
    RUNTIME DESTINATION bin
    )
    endforeach(EXAMPLE_SOURCE )
    endif()

    install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    )

    install(DIRECTORY /include/ DESTINATION include)
    install(EXPORT print-config DESTINATION cmake)

