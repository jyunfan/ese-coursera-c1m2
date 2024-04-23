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
#      make compile-all|build|clean|c1m2.map|c1m2.out
#
# Platform Overrides:
#      make PLATFORM=HOST|MSP432
#
#------------------------------------------------------------------------------
# default Platform
PLATFORM = HOST

include sources.mk

# Architectures Specific Flags
ifeq ($(PLATFORM),MSP432)
	LINKER_FILE = ../msp432p401r.lds
	CPU = -mcpu=cortex-m4 -mthumb
	ARCH = -march=armv7e-m -mfloat-abi=hard -mfpu=fpv4-sp-d16
	SPECS = --specs=nosys.specs
	LDFLAGS = -T $(LINKER_FILE)
endif

CFLAGS = -Wall -Werror -g -O0 -std=c99 $(INCLUDES)

# Compiler Flags and Defines
ifeq ($(PLATFORM),HOST)
	CC = gcc
	CFLAGS := $(CFLAGS) $(CPU) $(ARCH) $(SPECS) -DHOST
	# etc
else
	CC = arm-none-eabi-gcc
	CFLAGS := $(CFLAGS) $(CPU) $(ARCH) $(SPECS) -DMSP432
	# etc
endif

LD = 
CPPFLAGs = 

.PHONY: compile-all
compile-all: $(SOURCES)
	$(CC) $(CFLAGS) -c $(SOURCES)

.PHONY: dependency
dependency: $(SOURCES)
	$(CC) $(CFLAGS) -MM -MD -E $(SOURCES)

.PHONY: build
build: $(SOURCES)
	make dependency
	make compile-all
	$(CC) $(CFLAGS) $(LDFLAGS) -Xlinker -Map=c1m2.map -o c1m2.out $(SOURCES)

.PHONY: clean
clean:
	rm -f *.o *.out *.map *.i *.asm *.d

%.o: %.c
	$(CC) $(CFLAGS) -c $^ -o $@

%.i: %.c
	$(CC) $(CFLAGS) -E $^ -o $@

%.asm: %.c
	$(CC) $(CFLAGS) -S $^ -o $@

%.d: %.c
	$(CC) $(CFLAGS) -MM $^ -o $@

c1m2.map:

c1m2.out: 
	$(CC) $(CFLAGS) $(LDFLAGS) -o c1m2.out $(SOURCES)

