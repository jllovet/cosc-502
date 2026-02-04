# COSC 502 - Computer Organization and Architecture - Claude Context

Course assignments, notes, labs, and projects for Computer Organization and Architecture at Towson University.

---

## Critical Rules

| Rule | Details |
|------|---------|
| **Read before edit** | ALWAYS read existing code/documents before modifying |
| **Conventional commits** | Use `feat:`, `fix:`, `chore:`, `docs:` prefixes |
| **ISO-8601 dates** | Use ISO-8601 format for dates (YYYY-MM-DD) |
| **Compile before commit** | LaTeX documents must compile; assembly must assemble |
| **Test circuits** | Verify Logisim/TinkerCAD circuits work before saving |

---

## Project Overview

**Course:** COSC 502 - Computer Organization and Architecture
**Semester:** Spring 2026
**Textbook:** The Essentials of Computer Organization and Architecture, 6th Edition by Linda Null
**Tech Stack:** LaTeX (Docker-based builds), x86-64 Assembly (NASM), Logisim, TinkerCAD
**Repository Type:** Academic coursework (assignments, labs, notes, projects)

### Course Topics

- Digital logic fundamentals (gates, Boolean algebra)
- Combinational circuits (adders, ALUs, multiplexers)
- Sequential circuits (flip-flops, registers, counters)
- Computer architecture (von Neumann, instruction sets)
- x86-64 assembly programming
- Memory hierarchy and cache
- I/O and interrupts
- Pipelining and optimization

### Supplementary Lab Curriculum

This repository includes a self-directed lab curriculum with hands-on projects. See `supplementary-lab-curriculum/` for:
- TinkerCAD circuit labs
- Logisim digital design projects
- x86-64 assembly programming exercises
- Research papers on computer architecture topics

---

## Project Structure

```
.
├── assignment-X/              # Assignment submissions
│   ├── main.tex              # LaTeX source
│   ├── main.pdf              # Compiled output
│   └── src/                  # Code (assembly, etc.)
├── supplementary-lab-curriculum/
│   ├── lab-curriculum.md     # Full curriculum overview
│   ├── module-01-.../        # Digital logic fundamentals
│   ├── module-02-.../        # Combinational logic
│   ├── ...
│   └── module-09-.../        # Capstone project
├── resources/
│   └── assignment-template.tex
├── Dockerfile                # TeX Live 2025 image
├── docker-compose.yml
└── Makefile                  # Build helpers
```

---

## Tool Workflows

### LaTeX (Documentation & Assignments)

```bash
# Build with Docker
make build FILE=assignment-X/main.tex

# Watch for changes
make watch FILE=assignment-X/main.tex

# Clean auxiliary files
make clean
```

### x86-64 Assembly (NASM)

```bash
# Assemble
nasm -f elf64 -o program.o program.asm

# Link
ld -o program program.o

# Run
./program

# Debug with GDB
gdb ./program
```

### Logisim

- Save circuits as `.circ` files in the appropriate lab folder
- Use Logisim Evolution for better features: https://github.com/logisim-evolution/logisim-evolution
- Test all input combinations before considering a circuit complete

### TinkerCAD

- Export screenshots of completed circuits
- Document truth tables alongside circuit screenshots
- Save shareable links in lab notes

---

## Common LaTeX Patterns

For circuit diagrams, use circuitikz:
```latex
\usepackage{circuitikz}
\begin{circuitikz}
  \draw (0,0) node[and port] (and1) {}
        (and1.in 1) node[left] {A}
        (and1.in 2) node[left] {B}
        (and1.out) node[right] {Y};
\end{circuitikz}
```

For truth tables:
```latex
\begin{tabular}{cc|c}
A & B & Y \\
\hline
0 & 0 & 0 \\
0 & 1 & 0 \\
1 & 0 & 0 \\
1 & 1 & 1 \\
\end{tabular}
```

For assembly code listings:
```latex
\usepackage{listings}
\lstset{language=[x86masm]Assembler}
\begin{lstlisting}
section .text
global _start
_start:
    mov rax, 60    ; syscall: exit
    xor rdi, rdi   ; status: 0
    syscall
\end{lstlisting}
```

---

## Issue Tracker Integration (Linear)

### Setup

```bash
# Install Linear CLI
go install github.com/jllovet/linear-cli@latest

# Environment variables
export LINEAR_API_TOKEN="your-token"
export LINEAR_DEFAULT_TEAM="TU"

# Load environment
direnv allow && eval "$(direnv export bash)"
```

### Common Commands

```bash
# List assignments/tasks
linear issues list --team TU

# Get issue details
linear issues get --id TU-123

# Update state
linear issues assign state --issue TU-123 --to "In Progress"
linear issues assign state --issue TU-123 --to "Done"

# Add comment
linear issues comment --id TU-123 --body "Completed lab 2.1"
```

### Labels

| Label | Use For |
|-------|---------|
| `type-assignment` | Course assignments |
| `type-lab` | Hands-on lab work |
| `type-notes` | Lecture notes |
| `type-paper` | Written papers |
| `type-project` | Programming projects |
| `course-cosc502` | This course |

---

## Autonomous Permissions

Claude may perform these operations **without asking**:

### Environment & Git (Safe)
| Action | Examples |
|--------|----------|
| **direnv** | `direnv allow`, `eval "$(direnv export bash)"` |
| **Fetch/Pull** | `git fetch`, `git pull` |
| **Status** | `git status`, `git log`, `git diff` |
| **Commit** | `git add`, `git commit` |
| **Push** | `git push` |

### Build Operations
| Action | Examples |
|--------|----------|
| **LaTeX** | `make build FILE=...`, `make clean` |
| **Assembly** | `nasm`, `ld`, running test programs |

### Linear (Read/Update)
| Action | Examples |
|--------|----------|
| **Read** | List, get, search issues |
| **Update** | Update states, add comments |

**Requires confirmation:**
- Creating new Linear issues
- Deleting files
- Any destructive operations

---

## Development Patterns

### Commits

Use conventional commits:
- `docs:` - Assignment writeups, notes, papers
- `feat:` - New code/circuits/solutions
- `fix:` - Corrections to solutions
- `chore:` - Build config, cleanup
- `lab:` - Lab work (TinkerCAD, Logisim, assembly)

Example:
```
lab(module-02): complete 4-bit adder in Logisim

Built ripple-carry adder using full adder components.
Tested all 256 input combinations.

Co-Authored-By: Claude <noreply@anthropic.com>
```

### Pre-Commit Checks

See `skills/_shared/pre-commit-checks.md` for language-specific checks.

---

## Workflow Tips

### For Assignments

1. Create assignment directory: `assignment-X/`
2. Copy template: `cp resources/assignment-template.tex assignment-X/main.tex`
3. Update header (name, date, assignment number)
4. Build incrementally as you work
5. Update Linear issue when complete

### For Labs

1. Navigate to the appropriate module folder
2. Read the README.md for instructions
3. Complete the lab in the appropriate subfolder (tinkercad/, logisim/, assembly/)
4. Document your work with screenshots or comments
5. Test thoroughly before marking complete

### For Assembly Programming

1. Write clear comments explaining each section
2. Test with simple inputs first
3. Use GDB to debug: `gdb ./program`
4. Document register usage and calling conventions

### For Papers

1. Research using provided resources first
2. Use proper citations
3. Focus on understanding, not just summarizing
4. Include diagrams where helpful

---

## x86-64 Quick Reference

### Registers
| Register | Purpose |
|----------|---------|
| `rax` | Return value, syscall number |
| `rdi` | 1st argument |
| `rsi` | 2nd argument |
| `rdx` | 3rd argument |
| `rcx` | 4th argument (or loop counter) |
| `r8`, `r9` | 5th, 6th arguments |
| `rsp` | Stack pointer |
| `rbp` | Base pointer |

### Common Syscalls (Linux)
| Number | Name | Arguments |
|--------|------|-----------|
| 0 | read | fd, buf, count |
| 1 | write | fd, buf, count |
| 60 | exit | status |

---

## Core Principles

- **Understanding First**: Don't just memorize; understand the "why"
- **Hands-On Learning**: Build circuits and write code to reinforce concepts
- **Clear Documentation**: Comment your assembly, document your circuits
- **Iterative Testing**: Test small pieces before combining them
