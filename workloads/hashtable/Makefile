CC=g++
CFLAGS=-Wall -g -std=c++0x

.SUFFIXES: .o .c .h

SRC_DIRS = ./
DEPS = -I.

CFLAGS += $(DEPS) #-D  -Werror
CFLAGS_GEM5 = $(CFLAGS) -DGEM5
CFLAGS_PIM5 = $(CFLAGS_GEM5) -DPIM
LDFLAGS = -Wall -L. -pthread -g -lrt -std=c++0x
LDFLAGS += $(CFLAGS)
LDFLAGS_GEM5 = $(LDFLAGS) -DGEM5
LDFLAGS_PIM5 = $(LDFLAGS_GEM5) -DPIM

CPPS = $(foreach dir,$(SRC_DIRS),$(wildcard $(dir)*.c))
ASMS = $(foreach dir,$(SRC_DIRS),$(wildcard $(dir)*.S))

OGEM = $(addprefix gem5/, $(notdir $(CPPS:.c=.o))) $(addprefix gem5/, $(notdir $(ASMS:.S=.o)))
OPIM = $(addprefix pim5/, $(notdir $(CPPS:.c=.o))) $(addprefix pim5/, $(notdir $(ASMS:.S=.o)))

all:hashtable_gem5 hashtable_pim5

hashtable_gem5 : $(OGEM)
	$(CC) -o $@ $^ $(LDFLAGS_GEM5)
./gem5/%.o: %.c | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: %.S | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
gem5:
	mkdir -p gem5

hashtable_pim5 : $(OPIM)
	$(CC) -o $@ $^ $(LDFLAGS_PIM5)
./pim5/%.o: %.c | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: %.S | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
pim5:
	mkdir -p pim5

.PHONY: clean
clean:
	rm -rf gem5 pim5
