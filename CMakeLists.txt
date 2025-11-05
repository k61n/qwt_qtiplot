cmake_minimum_required(VERSION 3.18)

project(qwt VERSION 5.2.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

set(QT_MODULES Core Svg Widgets)
if (${PREFER_QT})
    set(V ${PREFER_QT})
    find_package(Qt${V} COMPONENTS ${QT_MODULES} REQUIRED)
else ()
    find_package(Qt6 COMPONENTS ${QT_MODULES} QUIET)
    if (${Qt6_FOUND})
        set(V 6)
    else ()
        find_package(Qt5 COMPONENTS ${QT_MODULES} REQUIRED)
        set(V 5)
    endif ()
endif ()

# if this project is not configured as a subproject
if (CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    message(STATUS "Found Qt: ${Qt${V}Core_VERSION}")
    foreach (module IN LISTS QT_MODULES)
        get_target_property(module_path Qt${V}::${module} LOCATION)
        message(STATUS "Found ${module}: ${module_path}")
    endforeach ()
endif ()

file(GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
file(GLOB_RECURSE HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/include/*.h")

if (MSVC)
    add_compile_options($<$<CXX_COMPILER_ID:MSVC>:/MP>)
endif ()

add_library(qwt_static STATIC ${SOURCES} ${HEADERS})
if (MSVC AND BUILD_SHARED_LIBS)
    add_definitions(-DQWT_MAKEDLL=1)
    set_target_properties(qwt_static PROPERTIES OUTPUT_NAME "qwt_static")
else ()
    set_target_properties(qwt_static PROPERTIES OUTPUT_NAME "qwt")
endif ()
target_include_directories(qwt_static PRIVATE ${PROJECT_SOURCE_DIR}/include)
foreach (module IN LISTS QT_MODULES)
    target_link_libraries(qwt_static PUBLIC Qt${V}::${module})
endforeach ()
target_link_libraries(qwt_static PUBLIC Qt${V}::Core Qt${V}::Svg Qt${V}::Widgets)

if (BUILD_SHARED_LIBS)
    add_library(qwt_shared SHARED $<TARGET_OBJECTS:qwt_static>)
    set_target_properties(qwt_shared PROPERTIES OUTPUT_NAME "qwt")
    target_include_directories(qwt_shared PRIVATE ${PROJECT_SOURCE_DIR}/include)
    foreach (module IN LISTS QT_MODULES)
        target_link_libraries(qwt_shared PUBLIC Qt${V}::${module})
    endforeach ()
endif ()

# if this project is not configured as a subproject
if (CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    include(GNUInstallDirs)
    install(TARGETS qwt_static
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
    if (BUILD_SHARED_LIBS)
        install(TARGETS qwt_shared
            LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
    endif ()
    install(FILES ${HEADERS}
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/qwt)
endif ()
