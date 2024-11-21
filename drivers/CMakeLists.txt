# Copyright (c) 2021 Nordic Semiconductor ASA
# Copyright (c) 2024 Microchip Technology Inc.
# SPDX-License-Identifier: Apache-2.0

# Out-of-tree drivers for custom classes
add_subdirectory_ifdef(CONFIG_BLINK blink)

# Out-of-tree drivers for existing driver classes
add_subdirectory_ifdef(CONFIG_SENSOR sensor)

# Out-of-tree driver for Introspect I3C analyzer
add_subdirectory_ifdef(CONFIG_INTROSPECT_I3C introspect_i3c)
