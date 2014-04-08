#
# Copyright (C) 2014 Pavel Kirienko <pavel.kirienko@gmail.com>
#

PROJECT = uavcan_test_stm32f107

#
# Test application
#

CPPSRC = src/main.cpp src/dummy.cpp

#
# UAVCAN library
#

UDEFS = -DUAVCAN_STM32_CHIBIOS=1         \
        -DUAVCAN_STM32_TIMER_NUMBER=6    \
        -DUAVCAN_STM32_DEBUG=1           \
        -DUAVCAN_MEM_POOL_BLOCK_SIZE=56

include ../../../libuavcan/include.mk
CPPSRC += $(LIBUAVCAN_SRC)
UINCDIR += $(LIBUAVCAN_INC)

include ../driver/include.mk
CPPSRC += $(LIBUAVCAN_STM32_SRC)
UINCDIR += $(LIBUAVCAN_STM32_INC)

# TODO: add target for this
$(info $(shell $(LIBUAVCAN_DSDLC) $(UAVCAN_DSDL_DIR)))
UINCDIR += dsdlc_generated

#
# Platform
#

CSRC += src/sys/board.c

UINCDIR += src/sys

SERIAL_CLI_PORT_NUMBER = 2

RELEASE_OPT = -Os -fomit-frame-pointer
DEBUG_OPT = -Os -g3
USE_OPT = -flto -u_port_lock -u_port_unlock -uchThdExit

include crdr_chibios/rules_stm32f105_107.mk