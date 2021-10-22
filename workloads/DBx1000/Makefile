CC=g++
CFLAGS=-Wall -g -std=c++0x

.SUFFIXES: .o .cpp .h .S

SRC_DIRS = ./ ./benchmarks/ ./concurrency_control/ ./storage/ ./system/
DEPS = -I. -I./benchmarks -I./concurrency_control -I./storage -I./system

CFLAGS += $(DEPS) -D NOGRAPHITE=1 -Werror
CFLAGS_GEM5 = $(CFLAGS) -DGEM5
CFLAGS_PIM5 = $(CFLAGS_GEM5) -DPIM
LDFLAGS = -Wall -L. -pthread -g -lrt -std=c++0x
LDFLAGS += $(CFLAGS)
LDFLAGS_GEM5 = $(LDFLAGS) -DGEM5
LDFLAGS_PIM5 = $(LDFLAGS_GEM5) -DPIM

CPPS = $(foreach dir,$(SRC_DIRS),$(wildcard $(dir)*.cpp))
ASMS = $(foreach dir,$(SRC_DIRS),$(wildcard $(dir)*.S))

#CPPS = $(wildcard *.cpp)
OGEM = $(addprefix gem5/, $(notdir $(CPPS:.c=.o))) $(addprefix gem5/, $(notdir $(ASMS:.S=.o)))
OPIM = $(addprefix pim5/, $(notdir $(CPPS:.c=.o))) $(addprefix pim5/, $(notdir $(ASMS:.S=.o)))

#NOGRAPHITE=1

all:rundb_gem5 rundb_pim5

rundb_gem5 : $(OGEM)
	$(CC) -o $@ $^ $(LDFLAGS_GEM5)
./gem5/%.o: benchmarks/%.cpp | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: storage/%.cpp | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: system/%.cpp | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: system/%.S | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: concurrency_control/%.cpp | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: %.cpp | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
./gem5/%.o: %.S | gem5
	$(CC) -c $(CFLAGS_GEM5) $(INCLUDE) -o $@ $<
gem5:
	mkdir -p gem5

rundb_pim5 : $(OPIM)
	$(CC) -o $@ $^ $(LDFLAGS_PIM5)
./pim5/%.o: benchmarks/%.cpp | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: storage/%.cpp | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: system/%.cpp | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: system/%.S | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: concurrency_control/%.cpp | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: %.cpp | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
./pim5/%.o: %.S | pim5
	$(CC) -c $(CFLAGS_PIM5) $(INCLUDE) -o $@ $<
pim5:
	mkdir -p pim5

.PHONY: clean
clean:
	rm -rf pim5 gem5
