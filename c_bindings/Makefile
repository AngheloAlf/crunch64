# Either `debug` or `release`
BUILD_MODE ?= debug

CC   := gcc
LIB  := ../target/$(BUILD_MODE)/libcrunch64.a

CSTD       := -std=c11
ifeq ($(BUILD_MODE), debug)
	CFLAGS ?= -O0 -g3
else
	CFLAGS ?= -Os
endif
IINC       := -I include
WARNINGS   := -Wall -Wextra -Wshadow -Werror


C_BINDINGS_TESTS := tests.c
C_BINDINGS_ELF   := tests.elf

all: $(C_BINDINGS_ELF)

clean:
	$(RM) $(C_BINDINGS_ELF)

.PHONY: all clean
.DEFAULT_GOAL := all

CARGO_FLAGS ?=
ifneq ($(BUILD_MODE), debug)
    CARGO_FLAGS += --release
endif
$(shell cargo build --lib --features c_bindings $(CARGO_FLAGS))


$(C_BINDINGS_ELF): $(C_BINDINGS_TESTS) $(LIB)
	$(CC) $(CSTD) $(CFLAGS) $(IINC) $(WARNINGS) -o $@ $< -L ../target/$(BUILD_MODE) -Wl,-Bstatic -l crunch64 -Wl,-Bdynamic

# Print target for debugging
print-% : ; $(info $* is a $(flavor $*) variable set to [$($*)]) @true
