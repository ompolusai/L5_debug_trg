ifeq ($(KERNELRELEASE),)  

#########################################
# To support cross-compiling for the ARM:
# For ARM, invoke make as:
# make ARCH=arm CROSS_COMPILE=arm-none-linux-gnueabi- 
ifeq ($(ARCH),arm)
# Update 'KDIR' below to point to the ARM Linux kernel source tree
KDIR ?= ~/DG-L3/linux-3.2.21
else
KDIR ?= /lib/modules/$(shell uname -r)/build 
endif
#########################################

PWD := $(shell pwd)  

.PHONY: build clean  

build:
	$(MAKE) -Wall -C $(KDIR) M=$(PWD) modules
install:
	$(MAKE) -C $(KDIR) M=$(PWD) modules_install
clean:
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) clean

else

$(info Building with KERNELRELEASE = ${KERNELRELEASE}) 
EXTRA_CFLAGS += -DDEBUG
obj-m :=    ioctl_kdrv.o  

endif

user_test: user_test.c
	${CROSS_COMPILE}gcc user_test.c -o ioctl_usertest -Wall -Os

