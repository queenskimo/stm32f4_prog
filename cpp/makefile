CFLAGS=-g
MYCFLAGS=-fno-common -O0 -g -mcpu=cortex-m3 -mthumb -fno-exceptions -fno-rtti -fomit-frame-pointer
MYCFLAGS_NO_LD=-nostartfiles -ffreestanding -fno-common -O0 -g -mcpu=cortex-m3 -mthumb
LD_FLAGS=-Wl,-T./stm32.ld -nostartfiles -fomit-frame-pointer

all: mycpp.bin

myp.elf: myp.o
	arm-none-eabi-g++ $(LD_FLAGS) -Wl,-Map,$@.map -o $@ $^

mycpp11.elf: mycpp11.o
	arm-none-eabi-g++ $(LD_FLAGS) -Wl,-Map,$@.map -o $@ $^
mycpp11.o: mycpp11.cpp stm32.h
	arm-none-eabi-g++ -std=c++11 $(MYCFLAGS) $(INC) -c $< 

%.o:%.S
	arm-none-eabi-g++ $(MYCFLAGS) $(INC) -c $< 

%.o:%.cpp
	arm-none-eabi-g++ $(MYCFLAGS) $(INC) -c $< 

new_section.o: new_section.cpp
	arm-none-eabi-g++ -fno-common -O0 -g -mcpu=cortex-m3 -mthumb -fomit-frame-pointer  -c new_section.cpp 


mycpp.o: mycpp.cpp stm32.h

mycpp.elf: mycpp.o new_section.o mem.o my_setjmp.o
	arm-none-eabi-g++ $(LD_FLAGS) -o $@ $^

alloc: alloc.cpp
	g++ -o $@ $<
%.bin:%.elf
	arm-none-eabi-objcopy -O binary $< $@

clean:
	rm -rf *.o *.bin *.elf
