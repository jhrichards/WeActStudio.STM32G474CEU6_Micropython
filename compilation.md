### Required software packages ###

git, dfu-util and gcc-arm-non-eabi

### Clone the repositories ###

Create a directory, let's say 'git', and change directory into it. Henceforth directories will be specified with this as the base.

Clone the Micropython and my cloned repositories

git clone https://github.com/micropython/micropython.git

git clone https://github.com/jhrichards/WeActStudio.STM32G474CEU6_Micropython.git

### Bleeding edge or stable release? ###

By default the Micropython repository exposes the master branch, you may prefer to compile against a stable release. Change directory to 'micropython', and enter the command 'git tag -l'. This will list the releases, as of writing the latest is 1.28.0

Enter the command 'git checkout v1.28.0', this will expose that tag.

The command 'git checkout master' will revert to the latest version.

Copy my files into the Micropython repository

Copy the following directory and its files  'WeActStudio.STM32G474CEU6_Micropython/WEACTG474CE/' into 'micropython/git/micropython/ports/stm32/boards/'

### Compilation ###

This follows the instructions in 'micropython/ports/stm32/README.md'.

Change directory to 'micropython'.

Execute the command 'make -C mpy-cross'

Change directory to 'micropython/ports/stm32'

Execute the command 'make BOARD=WEACTG474CE submodules'

Execute the command 'make BOARD=WEACTG474CE LTO=1'

The above command should produce binary images in the `build-WEACTG474CE`
subdirectory.

### Program the IC ###

Connect to the target board via USB, set it into DFU mode, and execute the following command.

'dfu-util -a 0 -D build-WEACTG474CE/firmware.dfu'

Reset the board and you should be able to connect to the Micropython REPL.
