SOURCES = $(wildcard *.mmd)
TARGETS = $(SOURCES:.mmd=.svg)

.PHONY: all
all: $(TARGETS)

%.svg: %.mmd
	mmdc -i $< -o $@
