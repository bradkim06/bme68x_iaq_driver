# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)

set(BOARD_ROOT ${CMAKE_SOURCE_DIR}) 
set(APP_ROOT ${CMAKE_SOURCE_DIR}) 
# BME68X IAQ Driver
list(APPEND ZEPHYR_EXTRA_MODULES
  ${CMAKE_CURRENT_SOURCE_DIR}/drivers
)

find_package(Zephyr 3.3.99 EXACT)
project(bme68x_iaq_sample)

# The common headers required for both the BME68x_IAQ driver and the application
zephyr_include_directories(include)

target_sources(app PRIVATE src/main.c)
