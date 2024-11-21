#-------------------------------------------------------------------------------
# Zephyr external application for MEC1753 I3C
#
# Copyright (c) 2024 Microchip Technology Inc.
# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.13.1)
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

project(app LANGUAGES C)

target_sources(app PRIVATE src/main.c)
