cmake_minimum_required(VERSION 3.18)

project(qwt VERSION 5.2.1)

set(CMAKE_CXX_STANDARD 17)
#set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

if (${PREFER_QT})
    if (${PREFER_QT} EQUAL 6)
        find_package(Qt6 COMPONENTS Core Svg Widgets REQUIRED)
        set(V 6)
    elseif (${PREFER_QT} EQUAL 5)
        find_package(Qt5 COMPONENTS Core Svg Widgets REQUIRED)
        set(V 5)
    endif ()
else ()
    find_package(Qt6 COMPONENTS Core Svg Widgets QUIET)
    if (${Qt6_FOUND})
        set(V 6)
    else ()
        find_package(Qt5 COMPONENTS Core Svg Widgets REQUIRED)
        set(V 5)
    endif ()
endif ()
get_target_property(QT_LIB_PATH Qt${V}::Core LOCATION)
message(STATUS "Found Qt${V}Core: ${QT_LIB_PATH}")

set(SOURCES
    src/qwt_abstract_scale_draw.cpp
    src/qwt_abstract_scale.cpp
    src/qwt_abstract_slider.cpp
    src/qwt_analog_clock.cpp
    src/qwt_arrow_button.cpp
    src/qwt_clipper.cpp
    src/qwt_color_map.cpp
    src/qwt_compass_rose.cpp
    src/qwt_compass.cpp
    src/qwt_counter.cpp
    src/qwt_curve_fitter.cpp
    src/qwt_data.cpp
    src/qwt_dial_needle.cpp
    src/qwt_dial.cpp
    src/qwt_double_interval.cpp
    src/qwt_double_range.cpp
    src/qwt_dyngrid_layout.cpp
    src/qwt_event_pattern.cpp
    src/qwt_interval_data.cpp
    src/qwt_knob.cpp
    src/qwt_layout_metrics.cpp
    src/qwt_legend_item.cpp
    src/qwt_legend.cpp
    src/qwt_magnifier.cpp
    src/qwt_math.cpp
    src/qwt_painter.cpp
    src/qwt_panner.cpp
    src/qwt_picker_machine.cpp
    src/qwt_picker.cpp
    src/qwt_plot_axis.cpp
    src/qwt_plot_canvas.cpp
    src/qwt_plot_curve.cpp
    src/qwt_plot_dict.cpp
    src/qwt_plot_grid.cpp
    src/qwt_plot_item.cpp
    src/qwt_plot_layout.cpp
    src/qwt_plot_magnifier.cpp
    src/qwt_plot_marker.cpp
    src/qwt_plot_panner.cpp
    src/qwt_plot_picker.cpp
    src/qwt_plot_print.cpp
    src/qwt_plot_printfilter.cpp
    src/qwt_plot_rasteritem.cpp
    src/qwt_plot_rescaler.cpp
    src/qwt_plot_scaleitem.cpp
    src/qwt_plot_spectrogram.cpp
    src/qwt_plot_svgitem.cpp
    src/qwt_plot_xml.cpp
    src/qwt_plot_zoomer.cpp
    src/qwt_plot.cpp
    src/qwt_raster_data.cpp
    src/qwt_round_scale_draw.cpp
    src/qwt_round_scale_draw.cpp
    src/qwt_scale_div.cpp
    src/qwt_scale_draw.cpp
    src/qwt_scale_engine.cpp
    src/qwt_scale_map.cpp
    src/qwt_scale_widget.cpp
    src/qwt_slider.cpp
    src/qwt_spline.cpp
    src/qwt_symbol.cpp
    src/qwt_text_engine.cpp
    src/qwt_text_label.cpp
    src/qwt_text.cpp
    src/qwt_thermo.cpp
    src/qwt_wheel.cpp)

set(HEADERS
    include/qwt_abstract_scale_draw.h
    include/qwt_abstract_scale.h
    include/qwt_abstract_slider.h
    include/qwt_analog_clock.h
    include/qwt_array.h
    include/qwt_arrow_button.h
    include/qwt_clipper.h
    include/qwt_color_map.h
    include/qwt_compass_rose.h
    include/qwt_compass.h
    include/qwt_counter.h
    include/qwt_curve_fitter.h
    include/qwt_data.h
    include/qwt_dial_needle.h
    include/qwt_dial.h
    include/qwt_double_interval.h
    include/qwt_double_range.h
    include/qwt_double_rect.h
    include/qwt_dyngrid_layout.h
    include/qwt_event_pattern.h
    include/qwt_global.h
    include/qwt_interval_data.h
    include/qwt_knob.h
    include/qwt_layout_metrics.h
    include/qwt_legend_item.h
    include/qwt_legend_itemmanager.h
    include/qwt_legend.h
    include/qwt_magnifier.h
    include/qwt_math.h
    include/qwt_painter.h
    include/qwt_panner.h
    include/qwt_picker_machine.h
    include/qwt_picker.h
    include/qwt_plot_canvas.h
    include/qwt_plot_curve.h
    include/qwt_plot_dict.h
    include/qwt_plot_grid.h
    include/qwt_plot_item.h
    include/qwt_plot_layout.h
    include/qwt_plot_magnifier.h
    include/qwt_plot_marker.h
    include/qwt_plot_panner.h
    include/qwt_plot_picker.h
    include/qwt_plot_printfilter.h
    include/qwt_plot_rasteritem.h
    include/qwt_plot_rescaler.h
    include/qwt_plot_scaleitem.h
    include/qwt_plot_spectrogram.h
    include/qwt_plot_svgitem.h
    include/qwt_plot_zoomer.h
    include/qwt_plot.h
    include/qwt_polygon.h
    include/qwt_raster_data.h
    include/qwt_round_scale_draw.h
    include/qwt_scale_div.h
    include/qwt_scale_draw.h
    include/qwt_scale_engine.h
    include/qwt_scale_map.h
    include/qwt_scale_widget.h
    include/qwt_slider.h
    include/qwt_spline.h
    include/qwt_symbol.h
    include/qwt_text_engine.h
    include/qwt_text_label.h
    include/qwt_text.h
    include/qwt_thermo.h
    include/qwt_valuelist.h
    include/qwt_wheel.h
    include/qwt.h)

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
target_link_libraries(qwt_static PUBLIC Qt${V}::Core Qt${V}::Svg Qt${V}::Widgets)

if (BUILD_SHARED_LIBS)
    add_library(qwt_shared SHARED $<TARGET_OBJECTS:qwt_static>)
    set_target_properties(qwt_shared PROPERTIES OUTPUT_NAME "qwt")
    target_include_directories(qwt_shared PRIVATE ${PROJECT_SOURCE_DIR}/include)
    target_link_libraries(qwt_shared PUBLIC Qt${V}::Core Qt${V}::Svg Qt${V}::Widgets)
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
