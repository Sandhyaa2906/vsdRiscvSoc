[1] Install & Sanity-Check the Toolchain
Objective: Set up the RISC-V toolchain and confirm binaries work.
 Steps:
 • Unpack the archive using tar.
 • Add the toolchain path to ~/.bashrc or terminal.
 • Confirm binaries like gcc, objdump, and gdb are accessible.
 Learning: Learned how to integrate a toolchain into your development environment and verify installation.
 Important Commands:
 tar -xzf riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
 export PATH=$HOME/riscv/bin:$PATH
 riscv32-unknown-elf-gcc --version

[2] Compile “Hello, RISC-V”
Objective: Write and cross-compile a minimal Hello World program for RV32IMC.
 Steps:
 • Write a hello.c file with printf("Hello, RISC-V\n");.
 • Use the RISC-V gcc to compile it with the appropriate flags.
 • Confirm the output binary is RISC-V ELF.
 Learning: Gained familiarity with cross-compiling using specific -march and -mabi flags.
 Important Command:
 riscv32-unknown-elf-gcc -march=rv32imc -mabi=ilp32 -o hello.elf hello.c

[3] From C to Assembly
Objective: Translate C source to assembly and understand stack setup.
 Steps:
 • Compile using -S -O0 to generate .s file.
 • Analyze generated assembly, focusing on function prologue/epilogue.
 Learning: Learned how stack pointer and return address are managed in RISC-V.
 Important Command:
 riscv32-unknown-elf-gcc -S -O0 hello.c

[4] Hex Dump & Disassembly
Objective: Disassemble ELF and extract raw hex data.
 Steps:
 • Use objdump to disassemble ELF.
 • Use objcopy to convert to Intel hex format.
 • Interpret address, opcode, mnemonic, and operands in disassembly.
 Learning: Learned to navigate binary file structures and analyze low-level code representation.

[5] ABI & Register Cheat-Sheet
Objective: Understand register naming and calling conventions in RV32.
 Steps:
 • Map x0–x31 to ABI names.
 • Learn which registers are caller/callee saved.
 Learning: Strengthened foundational knowledge for writing and debugging assembly code.

[6] Stepping with GDB
Objective: Debug RISC-V programs using gdb.
 Steps:
 • Launch riscv32-unknown-elf-gdb hello.elf.
 • Connect to target simulator and set breakpoint at main.
 • Step through execution and inspect registers.
 Learning: Learned to use GDB for instruction-level debugging.
 Important Commands:
 target sim,
 break main,
 run,
 info reg a0,
 disassemble

[7] Running Under an Emulator
Objective: Execute bare-metal ELF on QEMU or Spike.
 Steps:
 • Launch using spike or qemu-system-riscv32.
 • Use UART output to confirm program behavior.
 Learning: Understood how to simulate hardware behavior using emulators.
 Important Commands:
 spike --isa=rv32imc pk hello.elf
 or
 qemu-system-riscv32 -nographic -kernel hello.elf

[8] Exploring GCC Optimisation
Objective: Compare different optimization levels and understand their effects.
 Steps:
 • Compile the same C file with -O0 and -O2.
 • Analyze the differences in generated assembly.
 Learning: Observed optimizations like dead-code elimination and inlining in action.

[9] Inline Assembly Basics
Objective: Read hardware counters using inline assembly.
 Steps:
 • Write an inline assembly function to read CSR (cycle count).
 • Use constraints and qualifiers correctly.
 Learning: Learned syntax and semantics of inline assembly in GCC.
 Important Snippet:
 static inline uint32_t rdcycle(void) { uint32_t c; asm volatile ("csrr %0, cycle" : "=r"(c)); return c; }

[10] Memory-Mapped I/O Demo
Objective: Access a GPIO register in bare-metal C.
 Steps:
 • Create a volatile pointer to address 0x10012000.
 • Toggle the GPIO using direct memory access.
 Learning: Understood volatile and how it prevents compiler optimization.

