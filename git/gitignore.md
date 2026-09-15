# `.gitignore` для LaTeX

```gitignore
# Auxiliary files
*.aux
*.log
*.out
*.toc
*.lof
*.lot

# Bibliography
*.bbl
*.blg
*.bcf
*.run.xml

# latexmk
*.fdb_latexmk
*.fls

# SyncTeX
*.synctex
*.synctex.gz

# Index / glossary
*.idx
*.ind
*.ilg
*.glo
*.glg
*.gls
*.ist
*.acn
*.acr
*.alg

# Beamer
*.nav
*.snm
*.vrb

# Other generated files
*.dvi
*.xdv

# Temporary editor files
*~
*.bak
*.swp
*.tmp

# Do not usually ignore all PDFs:
# figures may be stored as PDF files.
#
# Ignore only the generated manuscript if needed:
# /article.pdf
```

# `.gitignore` для Python

```gitignore
# Virtual environments
.venv/
venv/
env/

# Python bytecode
__pycache__/
*.py[cod]
*$py.class

# Build / packaging
build/
dist/
*.egg-info/
.eggs/

# Tests and coverage
.pytest_cache/
.coverage
.coverage.*
htmlcov/

# Static analysis / formatter caches
.mypy_cache/
.pyright/
.ruff_cache/

# Jupyter
.ipynb_checkpoints/

# Environment files and local secrets
.env
.env.*
!.env.example

# Temporary editor files
*~
*.bak
*.swp
*.tmp
```

# `.gitignore` для Fortran в Visual Studio

```gitignore
# Visual Studio local workspace
.vs/

# Per-user Visual Studio files
*.suo
*.user
*.userosscache
*.sln.docstates

# Build directories
[Dd]ebug/
[Rr]elease/
x64/
x86/

# Other build configurations
[Dd]ebug*/
[Rr]elease*/

# Fortran compiler output
*.obj
*.mod
*.smod

# Executables and libraries
*.exe
*.dll
*.lib
*.exp

# Debugging and linker files
*.pdb
*.ilk
*.idb
*.ipdb
*.iobj

# Visual Studio intermediate files
*.tlog
*.lastbuildstate
ipch/
*.pch

# Temporary editor files
*~
*.bak
*.swp
*.tmp

# Keep project files in Git:
# *.sln
# *.vfproj
# *.vcxproj
# *.props
# *.targets
```
