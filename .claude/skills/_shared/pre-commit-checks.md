# Pre-Commit Checks

Run these checks **before** `git add` / `git commit`. Fix any issues before committing.

## Quick Reference

| Changed files in... | Run before committing |
|---------------------|----------------------|
| LaTeX (`.tex`) | `make build FILE=path/to/file.tex` |
| Assembly (`.asm`) | `nasm -f elf64 file.asm` |
| Logisim (`.circ`) | Open in Logisim, verify functionality |
| Python | `black . && isort . && flake8` |
| JSON/YAML config | Validate syntax |

## Language-Specific Checks

### LaTeX Documents

Run compilation to catch errors before committing:

```bash
# Using the project's Docker setup
make build FILE=assignment-X/main.tex

# Or direct Docker
docker compose run --rm latex path/to/file.tex
```

Common LaTeX errors to watch for:
- Missing `\end{}` tags
- Undefined control sequences
- Missing packages
- Math mode errors (unmatched `$`)
- BibTeX citation errors

### x86-64 Assembly (NASM)

```bash
# Assemble to check for syntax errors
nasm -f elf64 -o program.o program.asm

# Link to verify symbols
ld -o program program.o

# Run to test functionality
./program
echo $?  # Check exit code
```

Common assembly errors to watch for:
- Missing section declarations (`.text`, `.data`)
- Incorrect register sizes (e.g., using `eax` when you need `rax`)
- Missing `global _start` directive
- Incorrect syscall numbers or arguments
- Stack alignment issues (16-byte alignment for calls)

### Logisim Circuits

Before committing `.circ` files:
1. Open in Logisim Evolution
2. Test all input combinations
3. Verify expected outputs
4. Check for unconnected wires (yellow highlights)
5. Ensure subcircuits are properly named

### TinkerCAD Circuits

Before documenting TinkerCAD work:
1. Test all input combinations using switches
2. Verify LED outputs match truth table
3. Take screenshots with clear labeling
4. Export shareable link

### Python

```bash
black .
isort .
flake8
# Or using ruff:
ruff check --fix .
ruff format .
```

## General Rules

1. **Fix issues in files you modified** - Don't commit code that fails compilation
2. **LaTeX warnings are OK** - Overfull/underfull boxes can often be ignored
3. **Run tests if applicable** - `make test`, `./program`, etc.
4. **Check for secrets** - Never commit API keys, passwords, or credentials
5. **Verify output** - For LaTeX, check the PDF; for circuits, check functionality
6. **Assembly must run** - If it doesn't assemble and link, don't commit
