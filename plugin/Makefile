# PS3 Bluetooth Plugin Makefile
CELL_SDK ?= /usr/local/cell
CELL_MK_DIR ?= $(CELL_SDK)/samples/mk
include $(CELL_MK_DIR)/sdk.makedef.mk

PRX = btfix
PPU_SRCS = main.c
PPU_LDLIBS = -lfs_stub
PPU_CFLAGS += -O2

include $(CELL_MK_DIR)/sdk.target.mk