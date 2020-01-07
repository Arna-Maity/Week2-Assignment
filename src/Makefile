#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# <Put a Description Here>
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <Put a description of the supported targets here>
#
# Platform Overrides:
#      <Put a description of the supported Overrides here
#
#------------------------------------------------------------------------------
include sources.mk

# Platform Overrides
PLATFORM = MSP432

# Architectures Specific Flags
LINKER_FILE = ../msp432p401r.lds
CPU = cortex-m4
ARCH = thumb
MARCH = armv7e-m 
SPECS = nosys.specs

# Compiler Flags and Defines
CC = /usr/bin/arm-none-eabi-gcc
LD = /usr/bin/arm-none-eabi-as
TARGET = main
LDFLAGS = -Wl,-Map=$(TARGET).map -T $(LINKER_FILE)
CFLAGS = -mcpu=$(CPU) -march=$(MARCH) -m$(ARCH)  --specs=$(SPECS) -Wall -Werror -g -O0 -std=c99
CPPFLAGs = -D$(PLATFORM)

OBJS = $(SOURCES:.c=.o)

%.i : %.c
	$(CC) -E -I$(INCLUDES) -I$(INCLUDES_MSP432) -I$(INCLUDES_CMSIS) $(CPPFLAGs) $^ -o $@

%.o : %.i
	$(CC) -c $(CFLAGS) $(CPPFLAGs) $^ -o $@

#.PHONY: compile-all
#compile: $(OBJS)
	

#%.o : %.c
#	$(CC) -c $(CFLAGS) $< -o $@
