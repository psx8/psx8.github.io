TARGET_VERSIONS = 700 750 800 850 900 903 950
ENTRY = 0x900000000

CC = gcc
OBJCOPY = objcopy
CFLAGS = -O -Wno-int-conversion -fno-strict-aliasing -masm=intel -nostartfiles
CFLAGS += -fwrapv -no-pie -Ttext=$(ENTRY) -Tscript.ld -Wl,--build-id=none
CFLAGS += -fwrapv-pointer -std=gnu11

.PHONY: all
ALL_SOURCES = $(TARGET_VERSIONS:%=%.c)
ALL_OBJECTS = $(TARGET_VERSIONS:%=%.o)
ALL_BINS = $(TARGET_VERSIONS:%=%.bin)

all: $(ALL_BINS)

%.bin: %.o
	$(CC) $< -o $*.elf $(CFLAGS)
	$(OBJCOPY) -O binary --only-section=.text $*.elf $@
	-rm -f $*.bin

.PHONY: clean
clean:
	-rm -f $(ALL_OBJECTS) $(ALL_BINS)
