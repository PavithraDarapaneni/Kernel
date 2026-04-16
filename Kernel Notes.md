## OPerating System :
Bring up all the devices and provide a human interface.

Types : 1.Genaral Purpose -> windows,Linux(not time bound,no priority) 2.Real time -> RT Linux, FreeRTOS, VXWorks(Time bound based on priority)
Sheduler :Schedules the next task to be executed.

Types :
1.Round Robin :All tasks get equal amount of time to execute. scheduler maintains all the tasks in a linked list. Each node in the linked list get equal amount of time to execute.

Advantages : Every task will get time to executed.

Disadvantage : No priority will given to any task in round robin.

2.Pre-emptive Priority Based Scheduler :Higher priority task executes first.

Disadvantage : There is a posibility of low priority task may get delayed or isolated untill the high priority tasks gets executed.

Booting Process :CPU have a defined address to start the execution form. First address - 1st stage of boot loader(BIOS). purpose of 1st stage boot loader : Basic system configuration. Address -> Next stage of booting process. The next stage after the first loader booting process may be 2nd stage boot loader/OS.

## What is the purpose of 2nd stage boot loader ?
1.Choice of os if multiple os are installed 2nd stage boot loader is optional and it comes when it requires.
2.Select boot mode : Normal /safe mode/ command prompt mode second stage bootloader is optional.

Examples of 2nd stage boot loader : Windows boot,Linux GRUB,U-Boot.

main.c display.c display.h
Make file :
SRC = main.c display.c
Target is a label which is used to give as an argument to makefile to execute it. Target 1: dependencies gcc main.c display.c Target 2: Target 3 : . .
make / make (optional)

If there is no option argument in the make command the first argument is execute first. If a target mentions dependencies the absence of dependent component will makes the target fail. The statement return below target is only considered when there is atab intendations

Ex: Target : dependencies gcc main.c display.c command1 command2 gcc main.c display.c -o mainapp -> it creates custom file

Dependencies are opitonal if you give then the dependencies should be there if not make the target file. We can give like this also by using SRC macro gcc $(SRC) -o mainapp

'#' is used to command the line in makefile.
Src :

main.c

display.c Inc :

display.h

## Find all the files with .c and its extension SRC = $(shell find -name '*.c)

To execute shell command from make file use shell command.

To remove make file : rm -f executablefile

Inc : #include "display.h" It is in user defined location. user defined location : By default it is in current working directory if not spacified by user. #include<> : seraches the header in predefined location and location specified by the user. #include" " : First seraches in user defined location if not found then it will serach in the predefined location.

Make file :

all :
     gcc ./src/main.c ./src/display.c  -I ./inc -o mainapp
-I used to indicate include folders. src : main.c
 #include<stdio.h>
#include "display.h"

void main(){
        display("Hello world\n");
}
display.c

#include<stdio.h>

void display(char *buffer){
        printf("%s\n",buffer);
}
inc : display.h

#ifndef _DISPLAY_H
#define _DISPLAY_H

void display(char *buffer);

#endif
Make file :

SRC : ./src/main.c  ./src/display.c
INC : ./inc
all :
     gcc $(SRC) -I$(INC) -o mainapp
clean :
      rm -f mainapp
src (Directory)
lib1
lib2
lib3
mainapp
Cmake :
CMakeLists.txt inside the source tree
contents :
commands to define project,add source,includes and executable

projects() #optional

set(<src_variable_name>....)#mandatory

Include_directories( inc_dir1/ inc_dir2/ . .)

Add_executable(<targest name/output file name>${src_variable_name})

create a bulid directory out of souce tree

Enter inside the build directory and execute :

Cmake<path/to/source/tree>

Cmake scans the contents of CMakeLists.txt to generate Makefile based on the source tree

.a = static library file ,it doesnot have main function.

Libraries name always start with lib.

## If we have sorce code,how to generate sorce code?
main.c display.c display.c

gcc main.c display.c

Libdisplay.a lib display.a

gcc main.c-L/path/to/library-ldisplay

-L is used to provide the path of library.
. -> current working directory.
l -> link the library.
Compile the file only till the object generation. gcc -c display.c -> display.o For converting display.o to display.a ar -rc <libraryname.a> <objectfile.o> ar -> command Ex : ar -rc libdisplay.a display.o

display.h :
#ifndef _DISPLAY_H
#define _DISPLAY_H

void display(char *buffer);

#endif
main.c :
#include<stdio.h>
#include "display.h"

void main(){
        display("Hello world\n");
}
display.c :
#include<stdio.h>

void display(char *buffer){
        printf("%s\n",buffer);
}
gcc -c display.c -> display.o ar -rc libdisplay.a display.o -> libdisplay.a gcc main.c -L. -l display -> a.out

Project top level
src
mainapp -> Main.c
disp -> display.c
inc
disp -> display.h
Build_directory
Each and every folder and subfolder will need to have CMakeLists.txt.
CMAKE_SOURCE_DIR -> path to source tree.
CMAKE_BINARY_DIR -> path to build dircetory.
add_subdirectory(<DIR_NAME) add_subdirectory(src)

display.c will be compiled to generate libdisplay.a and main.c will be compiled and main.c linked to libdisplay.a.
Library creation :
add_library(<LIB_NAME>SRC) addlibrary(display display.c) -> it generates libdisplay.a

Linking Libraries :
target_link_libraries(<OUTPUT_FILE><LIB_NAME>) target_link_libraries(mainapp display)

Never write an absolute path in CMakeList.txt because these paths are changed.

Use the reference of macros to access source directory path and build directory path.

Similar source tree will be generated in the build directory and all the corresponding libraries will be placed in the corresponding location.

Binaries which are not executable are called as archives.Ex:static library

Binaries which are executable are called as run time outputs.

To specify generation of runtime outputs and archeives : set(CMAKE_RUNTIME_OUTPUT_DIRECTORY 
C
M
A
K
E
B
I
N
A
R
Y
D
I
R
/
B
i
n
)
s
e
t
(
C
M
A
K
E
A
R
C
H
I
V
E
O
U
T
P
U
T
D
I
R
E
C
T
O
R
Y
{CMAKE_BINARY_DIR}/Lib)

Top level CMakeLists.txt will have instructions to be executed before compilation and move to subdirectories to scan another CMakeLists.txt for further instructions.

add_executable(mainapp main.c file2.c file3. file4.c ...)

addexecutable use this souce file is to execute and remaining files are dependencies.
Cmake eases the creation of makefiles in a complex architectured source code.
Compilers :
compilers translates high level language to machine understandable language.

Based on architectures :
Native/host compiler :
Being on a machine, compiles for same machine.

Cross compiler :
Being aon a machine, compiles for different machine.

And generated code was not compiled on the own machine.

Either OS is differentor processor architecture is different.

This process is called cross compilation and the corresponding compiler is called cross compiler.

whenever we are compiling for the different machine we are refering to that machine called target.

X86/X64 -> intel architecture

Target -> any architecture (arm,power pc,bare meta,Linux based,RTOS based)

c/c++ :
Unbuntu -> gcc(c compiler) and g++ (cpp compiler) Install gnu compilers : sudo apt-get install build-essentials

For cross compilation we have to consider :

Hardware architecture
Vendor/Manufacture
software SDK -> software development kit

It have libraries specific to controller/processor and cross compilation.

Vendors and manufactures have their to supply the libraries and cross compilers.

Libraries and cross compilers are mandatory for the cross compilations.

For cross compilations : Preparing the build using cross compilers 1.path to the cross compiler. 2.Full label/name of the cross compiler.

CMAKE_C_COMPILER >> indicates tool for c compiler. CMAKE_CXX_COMPILER >> indicates tool for c++ compiler.

These two compilers (c and c++) indicates /user/bin path.

For cross compilation,modify these above macros (c and c++) with path of cross compiler.

cmake seraching and checking gcc and g++ in default whether present or working or not.

create .cmake file to provide the instructions to set cross compilation.

cmake -DCMAKE_TOOLCHAIN_FILE = /path/to/cmake -toolchain.cmake ../path/to project/src

Above command is used to set the cross compilation path.

To remove cmake file rm -rf *

## Steps for cross compilation :
1.create cmake-toolchain.cmake in top-level directory.
2.set the path of the compiler set(CC_TOOL_PATH /home/username/ti-preprocessor-sdk-linux-arm5-xx -evm-08_02_01_00/linux-devkit/sysroots/x86-64-argo-linux) path present in ti-processor-sdk-linux-am57xx-evm_08_02_01_00/linux-devkit/sysroots/x86_64_argo -linux/usr/bin set(CMAKE_C_COMPILER ${CC_TOOL_PATH}/usr/bin/arm-none-linux-gnueabihf-gcc)
3.Goto build directory username/build_math $ cmake -DCMAKE_TOOLCHAIN_FILE=../project_math/cmake-toolchain.cmake. cmake takes the instruction from cmake-toolchain.cmake before starting build. Executable mainapp present in the Bin directory.

## Linux :
Linux Subsystems :
Process management
Memory management
Network management
Device management
File I/O management
Single program that controls all the subsystems is called Linux-Kernel.

On kernel,we will focus on device management subsystem.

Every component is accessible through individual dedicated file.

File systems in Linux :
/etc/
/boot/
/dev/
/sys/
/var/
/lib/
/usr/
/proc/
For accessing device management subsystem /dev/ and /sys/ is used.

Except boot, all these file systems are temporary.

These file systems cannot be found on harddisk or hard drive.

These files systems are loaded only when Linux boots up.

Linux kernel loads these file systems.

They are created dynamically and loaded by Linux-kernel.

Virtual File Systems Loaded by the Kernel
Filesystem	Purpose
/dev/	Character device files
/sys/	Platform device entities
/proc/	Runtime process details
All these files system are temporary there are not present in the harddisk.

Linux loads these file systems at boot up time.

Why we need to configure/compile kernel ?
Configure the kernel according to the peripherals present in the target board.

Drivers for the hardware which are not present in the target board should be removed from the kernel.

We are scalling down the size of kernel by removing unneccessary drivers.

Configuration is done before the compilation process.

Current running kernel will not have any effect of the configuartion changes.

1.Configure the kernel -> Linux source code
2.Compile the kernel
reflect the changes
Compile according to the hardware architecture
3.Deployment (Install) the kernel.
Prerequisities :
make utility compiler tool chain -> host/cross

For required packages :

sudo apt-get install build-essentials
Primary purpose of the kernel configuration to remove or add drivers.
kconfig file
Provides the details of the driver

.config file
Keeps the information/track of saved configuration

Device tree files
Individual driver specifications

Download the Linux kernel source code from www.kernel.org

For checking kernel versions we use

  uname -r
Extract the source code from tar file
  tar -xvf <version>.tar.xz
In Linux version we have so many folders.From that folders we are concentrating on drivers and arch folders. Programs,kernel and other software components should be compact as much as possible. Due to limited storage size in embedded devices.

1.configuration :
make menuconfig
make menuconfig provides as interactive userspace to add/remove the components.

make menuconfig requires ncurses library.

symbols :
Symbol	Meaning
* or <Y>	Built-in
<M>	Loadable module
[ ] or <N>	Excluded
make _defconfig
Standard board manufactures will provide configuration files to quickly configure the linux kernel source according to their boards.

make < > defconfig applies the configuration from the file defconfig file. Eg :

make raspi_defconfig
Save the Configuration

Saved into:

.config
If you don't have defconfig then we can go through make menuconfig.

make menuconfig presents list of drivers which are part of kernel source code.

'*' -> The driver or component which is marked as star will be compiled and integrated to the kernel and are also called as buildin modules.
Buildin drivers cannot be removed from the running kernels.

Buildin drivers are part of kernel binary.

'M' -> Removable modules
Removable modules will be compiled and seperate binary will be created for corressponding driver or module.

Removable modules can be installed or removed from the kernel at any point of time.

' ' -> Excluded from compilation.

-> Build-in

-> Excludes

-> Modularize features

[*] -> build-in

[ ] -> excluded

-> Module

< > -> Module capable

once the configuration done save the configuration before exiting make menuconfig.

ls -a -> To see the hiodden files or files ends with '.'.
make menuconfiguration or defconfiguration the configuration are saved .config file.

Whenever we are compiling the kernel which module is build in /removable / excludes all the three will be scanned from .config file.

Compilation :
Legendery :
make -> build kernel & *marked modules

make modules -> build modules marked as M

make modules_install -> Install all removable modules(M)

make install -> Install the newly generated kernel

make                # kernel + built-in modules
make modules        # build M modules only
make modules_install
make install
New Kernel :
make -> build kernel and * marked modules

make module_install -> build and install all removable module(M)

make install -> Install the newly generated kernel

make
make modules_install
make install
All these commands can be executed from the top level directory only.

make install -> creates an entry in /etc/default/grub

GRUB helps to select the operating system to be booted.

At the boot up time GRUB shows the list of operating system to be selected.

Bootloader (GRUB)
make install
sudo update-grub -> refreshes the grub menu
make install updates:

/etc/default/grub
Then refreshes :

sudo update-grub
def config :
From top level directory we have to go to /linux version/arch/arm/config

here config -> all def config files are present in this folder

Any new defconfig is placed in this folder only.

High light the driver and press ? to get the details of driver.

Types defines the states

This driver have two states

'*' - Y
[] - n
prompt :
short description given to the driver in make menuconfig.

Location :
Indicates the location of driver i make menuconfig.

Defined at :
It actually shows the location of the kconfig file which is providing details of this driver.

make menuconfig is reading the kconfig files to list the drivers in the make menuconfig.

kconfig file is responsible to proviode the details of drivers to make menuconfig.

Each kconfig file will either provide the information of driver or paths to next kconfig file.

Execute make menuconfig and save it.

kconfig file provides the details of the particular driver along with configuration options in make menuconfig.

'*' in make menuconfig leads to y in .config.

'M' in make menuconfig leads to m in .config.

'[]' in make menuconfig leads to comment #.

The defconfig files also have similar macros when defconfig is applied the .config file will be updated according to the macros present in defconfig file.

Newly added driver must be populated in make menuconfig by updating its details in kconfig files.

Depends on indicates on which driver the current driver depends on.

To indicate a new driver kconfig files must be updated with the updated details of new driver.

If we use see/boot directory after compilation of kernel you find so may binaries.

kconfig file is used to integrate the driver into kernel.

After kernel compilation the name of binary generated Vmlinux.

Vmlinux ----> Vmlinuz

make install copy is the vmlinuz to /boot directory.

Vmlinuz is the actual kernel binary which loads when CPU boots

Kernel Binary Naming
Binary	Meaning
vmlinux	uncompressed kernel
vmlinuz	compressed kernel (loaded at boot)
Difference between user-application and Modules :
User Applications	Kernel Modules
main() entry	module_init()
no defined exit-point	module_exit()
user space RAM	kernel space RAM
console/GUI	device drivers
terminate with main()	stay resident until removed
A function is passed as an argument to module_init() macro is entry point of the modules.

Function passed as an argument to module_exit() macro is exit point.

Every device driver is a module but every module is not a driver.

Module waiting for request from hardware,another module.

Kernel cannot handle the errors in module.

Memory Leak :
When the address to dynamically allocated memory is lost before freeing it or before deallocating, it is called memory leak.

Invalid of pointers in the module, the system will be crashed. kernel doesnot handle these in modules.

For avoiding system crash :

if(*ptr != NULL){
      x=*ptr;
}
whenever you try to free the pointer , immmediately after freeing the pointer ,assign it to NULL.

free(ptr);
ptr=NULL;
Even if the module is removed , dynamically allocated memory which is not freed or deallocated remains in the kernel space of RAM.

In kernel space of RAM ensure the preservance of pointer pointing to dynamically allocated memory.

Use the exit() (or) exit point to freeup or deallocate all the resources allocated by the module.

Use global pointers, instead of local pointers to extend the scope.

Kernel build will be used to compile the modules or driver never use gcc

.c .c .c -> a.out/executable
.c .c .c -> .ko file
initialization function -> entry point Exit function -> exit point

Function to be created as an entry point should be passed as an argument to module_init() macro.

module_init(function name)
Function to be created as an exit point should be passed as an argument to module_exit() macro.

module_exit(function name)
printk() is used to print message in kernel log.

simple module :

#include <linux/init.h>
#include <linux/module.h>
#include <linux/kernel.h>

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Your Name");
MODULE_DESCRIPTION("Simple Linux Kernel Module");
MODULE_VERSION("1.0");

static int __init hello_init(void)
{
    printk(KERN_INFO "Hello Kernel! Module Loaded.\n");
    return 0;
}

static void __exit hello_exit(void)
{
    printk(KERN_INFO "Goodbye Kernel! Module Removed.\n");
}

module_init(hello_init);
module_exit(hello_exit);
For compilation of modules and drivers makefile is used. we need build to compile a module

build :
/lib/module/<kernel version>/build
Create a Makefile in the same folder
obj-m += hello_module.o

KDIR := /lib/modules/$(shell uname -r)/build

all:
	$(MAKE) -C $(KDIR) M=$(PWD) modules

clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean
To insert the moduke we have to use
sudo insmod <module_name.ko>
To see kernel logs
dmesg
check points to verify the module installation : Check the printk messages check proc file system
cat /proc/modules
lsmod
Whenever a module is installed it creates an entry in /proc/modules

Execute cat /proc/modules to see the installed module

We have another way to see installed module lsmod
lsmod # it shows list from /proc/modules only
To remove module
sudo rmmod hello_module
Module Entry and Exit Macros
In Linux kernel modules:

__init for entry

This indicates the function is used only during module initialization
After the initialization is complete, the function’s memory can be freed/offloaded to save RAM (important for embedded systems)
__exit for exit

This indicates the function is used only during module removal
If a module is built into the kernel (not loadable), this function will be discarded, as it’s not needed
MODULE_LINCENSE("GPL");
MODULE_AUTHOR("Author name");
