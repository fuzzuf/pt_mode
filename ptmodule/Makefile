obj-m += ptmodule.o
ptmodule-objs := proxy_mmap.o pt.o ptctl.o

all:
	$(MAKE) -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
	
clean:
	rm -f *.o *.ko
