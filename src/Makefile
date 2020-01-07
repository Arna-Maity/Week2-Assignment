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

TARGET = main

# General compiler flags for both platforms
CFLAGS = -Wall -Werror -g -O0 -std=c99

CPPFLAGs := -D$(PLATFORM)

# Compiler Flags and Defines
	ifeq ($(PLATFORM),MSP432)
		# Architectures Specific Flags
		LINKER_FILE := ../msp432p401r.lds
		CPU := cortex-m4
		ARCH := thumb
		MARCH := armv7e-m 
		SPECS := nosys.specs
		FPU := 

		CC := /usr/bin/arm-none-eabi-gcc
		LD := /usr/bin/arm-none-eabi-ld
		LDFLAGS := -Wl,-Map=$(TARGET).map -T $(LINKER_FILE)
		CFLAGS := $(CFLAGS) -mcpu=$(CPU) -march=$(MARCH) -m$(ARCH)  --specs=$(SPECS)
		SOURCES:= $(SOURCES) interrupts_msp432p401r_gcc.c startup_msp432p401r_gcc.c system_msp432p401r.c

	else
		CC := /usr/bin/gcc
		LD := /usr/bin/as
		# etc
	endif

OBJS = $(SOURCES:.c=.o)

%.i : %.c
	$(CC) -E $(INCLUDES) $(CPPFLAGs) $< -o $@

%.o : %.i
	$(CC) -c $(INCLUDES) $(CFLAGS) $(CPPFLAGs) $< -o $@

$(TARGET).out : $(OBJS)
	$(CC)  $(LDFLAGS) -o $(TARGET).out $(OBJS) 

.PHONY: compile-all
compile-all: $(OBJS)
	
.PHONY: build
build: $(TARGET).out
	
.PHONY: clean
clean:
	rm -rf *.i *.o *.asm *.map *.out
