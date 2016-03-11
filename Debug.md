

# Introduction #

These are instructions for compiling and running tint2 in debug mode, to help us fix bugs we cannot reproduce.

# Requirements #
Please install the dependencies and download the tint2 sources as explain in the [Install#Install\_manually](Install#Install_manually.md) page.

# Compile in debug mode #

```
cd tint2-<LATEST-RELEASE>
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Debug -DCMAKE_VERBOSE_MAKEFILE=ON ../
make
```

# Run tint2 in debugger #

From the `build` directory, run:

```
gdb ./tint2
run
```

# Obtaining a stack trace #

If tint2 receives a signal or crashes, a `(gdb)` prompt will appear. If there is no prompt but tint2 is hanged, you can press Ctrl+C to interrupt execution manually and cause a prompt to appear.

In the prompt, type '`bt`' and press Enter; a stack trace will be displayed. For example:

```
^C
Program received signal SIGINT, Interrupt.
0x00007ffff5178633 in __select_nocancel () at ../sysdeps/unix/syscall-template.S:82
82	in ../sysdeps/unix/syscall-template.S
(gdb) bt
#0  0x00007ffff5178633 in __select_nocancel () at ../sysdeps/unix/syscall-template.S:82
#1  0x0000000000414f0b in main ()
(gdb) 
```

Copy this text and paste it in your bug report.

# Obtaining a core dump #

In the `(gdb)` prompt, run '`generate-core-file`'. A core.xxxxx file will be generated in the build directory. Exit gdb with the command '`q`'. Then compress the core dump and the tint2 executable like this:

```
zip core.zip core.*
zip core.zip tint2
```

You can provide us the core.zip file.

**Important**: the core dump will contain the entire memory contents of tint2, including the titles of the windows shown in the taskbar and possibly a section of the desktop background below tint2. Please make sure no personal or sensitive information is contained before sending the core dump to anyone.