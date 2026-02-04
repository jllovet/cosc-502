# Towson University - COSC 502 - Computer Organization and Architecture

This repository contains selections of my notes, labs, and projects for COSC-502, taken 2026-Spring.

## Resources

- **Textbook:** The Essentials of Computer Organization and Architecture, 6th Edition by Linda Null
- **Supplementary Curriculum:** See `supplementary-lab-curriculum/` for self-directed labs

## Tech Stack

| Tool | Purpose |
|------|---------|
| LaTeX (Docker) | Assignment writeups and documentation |
| NASM | x86-64 assembly programming |
| Logisim Evolution | Digital circuit simulation |
| TinkerCAD | Interactive circuit building |
| GDB | Assembly debugging |

## LaTeX Setup

This project uses Docker for LaTeX compilation, providing a consistent build environment without requiring a local TeX installation.

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [VSCode](https://code.visualstudio.com/) with [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension (recommended)

### First-Time Setup

Build the Docker image:

```bash
make build-image
```

### Usage

#### VSCode (Recommended)

1. Open any `.tex` file
2. Save the file to trigger auto-build
3. Press `Ctrl+Alt+V` (Mac: `Cmd+Opt+V`) to open PDF preview
4. Double-click in the PDF to jump to the corresponding source line

#### Command Line

```bash
# Compile a .tex file
make build FILE=assignment-0/main.tex

# Watch for changes and auto-rebuild
make watch FILE=assignment-0/main.tex

# Clean auxiliary files
make clean
```

## Assembly Setup (x86-64)

### Prerequisites

- NASM (Netwide Assembler)
- GDB (GNU Debugger)
- Linux environment (native, WSL, or VM)

### Installation

```bash
# Ubuntu/Debian
sudo apt install nasm gdb

# macOS (for cross-compilation or use Linux VM)
brew install nasm
```

### Usage

```bash
# Assemble
nasm -f elf64 -o program.o program.asm

# Link
ld -o program program.o

# Run
./program

# Debug
gdb ./program
```

## Logisim Setup

Download [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution/releases) for enhanced features over classic Logisim.

Save circuit files (`.circ`) in the appropriate module's `labs/logisim/` folder.

## Project Structure

```
.
├── assignment-X/                    # Assignment submissions
│   ├── main.tex                    # LaTeX source
│   ├── main.pdf                    # Compiled output
│   └── src/                        # Code (if applicable)
├── supplementary-lab-curriculum/    # Self-directed labs
│   ├── lab-curriculum.md           # Full curriculum overview
│   ├── module-01-.../              # Digital logic fundamentals
│   ├── module-02-.../              # Combinational logic
│   └── ...                         # Additional modules
├── resources/
│   └── assignment-template.tex     # LaTeX template
├── Dockerfile                      # TeX Live image
├── docker-compose.yml
└── Makefile                        # Build helpers
```

## Supplementary Lab Curriculum

The `supplementary-lab-curriculum/` directory contains a comprehensive self-study curriculum covering:

| Module | Topic | Tools |
|--------|-------|-------|
| 1 | Digital Logic Fundamentals | TinkerCAD, Logisim |
| 2 | Combinational Logic Circuits | TinkerCAD, Logisim |
| 3 | Sequential Logic Circuits | TinkerCAD, Logisim |
| 4 | Computer Architecture Fundamentals | Logisim |
| 5 | Introduction to x86 Assembly | NASM, GDB |
| 6 | x86 Memory and Stack | NASM, GDB |
| 7 | Advanced x86 and Optimization | NASM, GDB |
| 8 | Input/Output and Interrupts | TinkerCAD, Logisim, NASM |
| 9 | Capstone Project | All tools |

Each module includes:
- Detailed lab instructions
- Paper assignments
- Video lecture recommendations
- Reading resources

See `supplementary-lab-curriculum/lab-curriculum.md` for the complete curriculum.

## Template Features

The included template (`resources/assignment-template.tex`) demonstrates:

- Mathematical notation (equations, matrices, Greek letters)
- Tables (usable for truth tables, state transitions)
- TikZ diagrams (automata, graphs)
- Verbatim blocks for pseudocode
- Including PDFs and images

## Course Topics

- Digital logic fundamentals (gates, Boolean algebra)
- Combinational circuits (adders, ALUs, multiplexers, decoders)
- Sequential circuits (flip-flops, registers, counters)
- Computer architecture (von Neumann, RISC vs CISC)
- x86-64 assembly programming
- Memory hierarchy and cache
- I/O systems and interrupts
- Pipelining and CPU optimization
