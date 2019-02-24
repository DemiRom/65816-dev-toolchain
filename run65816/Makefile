
all: run65816 lib65816.build

.PHONY : all clean lib65816.build

clean:
	make -C lib65816 clean
	rm -f run65816

CCOPTS ?= -O2 -DEMULATE_READMODE_PINS

lib65816.build:
	make -C lib65816 CCOPTS="$(CCOPTS)"

run65816: run65816.c lib65816.build
	$(CC) $(CCOPTS) run65816.c -o run65816  -I lib65816 -I lib65816/lib65816 lib65816/src/lib65816.a 

