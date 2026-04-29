cmake_minimum_required(VERSION 3.13)
project(pico_w_keypad_led C CXX)

# This project source is Arduino-style C++.
# Keep this file as repository scaffold/documentation placeholder.
# Build with an RP2040 Arduino-compatible environment.

add_custom_target(info ALL
  COMMAND ${CMAKE_COMMAND} -E echo "Use Arduino-compatible RP2040 toolchain to build src/main.cpp"
)
