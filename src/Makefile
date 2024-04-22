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
include sources.mk

# Platform Overrides
PLATFORM = 

# Architectures Specific Flags
LINKER_FILE = 
CPU = 
ARCH = 
SPECS = 

CFLAGS = -I$(INCLUDES)

# Compiler Flags and Defines
ifeq ($(PLATFORM),HOST)
	CC = gcc
	CFLAGS := $(CFLAGS) -DHOST
	# etc
else
	CC = arm-none-eabi-gcc
	# etc
endif

LD = 
LDFLAGS = 
CPPFLAGs = 

.PHONY: compile-all
compile-all: $(SOURCES)
	$(CC) $(CFLAGS) -c $(SOURCES)

.PHONY: build
build: $(SOURCES)
	$(CC) $(CFLAGS) -o c1m2.out $(SOURCES)

.PHONY: clean
clean:
	rm -f *.o *.out *.map

%.o: %.c
	$(CC) $(CFLAGS) -c $^ -o $@

%.i: %.c
	$(CC) $(CFLAGS) -E $^ -o $@

%.asm: %.c
	$(CC) $(CFLAGS) -S $^ -o $@

%.d: %.c
	$(CC) $(CFLAGS) -M $^ -o $@

c1m2.map:

c1m2.out: 


