# Python Basics for Computational Techniques

[![Deploy Jupyter Book](https://github.com/crisnapatel/python-basics/actions/workflows/deploy.yml/badge.svg)](https://github.com/crisnapatel/python-basics/actions/workflows/deploy.yml)

**Live Site:** [https://crisnapatel.github.io/python-basics/](https://crisnapatel.github.io/python-basics/)

A beginner-friendly Python tutorial designed for **CHL7002: Computational Techniques for Chemical Engineers** students at IIT Delhi.

---

## What Is This?

This is an interactive [Jupyter Book](https://jupyterbook.org/) website that teaches Python fundamentals through the lens of numerical methods. The running example throughout the tutorial is the **falling parachutist problem** from your textbook (Chapters 1–5), which introduces Euler's method and demonstrates why programming is essential for engineering.

---

## Topics Covered

| Topic | Description |
|-------|-------------|
| **Try Python** | In-browser Python playground (JupyterLite) |
| **Parachutist Problem** | Running example with video & interactive simulation |
| **Data Types** | Integers, floats, strings, booleans |
| **Variables** | Assignment, naming, and operators |
| **Print & Comments** | Output and documentation |
| **Control Flow** | `if`/`else`, `for` loops, `while` loops |
| **Data Structures** | Lists, tuples, dictionaries, sets |
| **Iterators** | `range()`, `enumerate()`, `zip()` |
| **User Input** | Reading input from users |
| **Functions** | Defining and calling functions |
| **NumPy Basics** | Arrays, operations, broadcasting |
| **Common Errors** | Reading tracebacks, debugging tips |

---

## Interactive Features

- **🎮 Parachutist Simulation** — Adjust mass, drag, and time step to visualize Euler's method in action
- **🗺️ Mind Map** — Collapsible tree view of all Python concepts with code examples
- **🐍 Python Playground** — JupyterLite environment to run code directly in your browser (no installation)

---

## Quick Start

**For Students:** Just visit the [live site](https://crisnapatel.github.io/python-basics/) and start learning!

**For Developers/Contributors:**

Contributions are welcome! I'm happy to receive merge requests for improvements, fixes, or new content.

```bash
# Clone the repository
git clone https://github.com/crisnapatel/python-basics.git
cd python-basics

# Install dependencies (Python 3.11+ recommended)
pip install "jupyter-book<1.0" jupyterlite-sphinx jupyterlite-pyodide-kernel

# Build locally
jupyter-book build .

# Open _build/html/index.html in your browser
```

---

## Project Structure

```
python-basics/
├── index.md                 # Welcome page
├── try_python.md            # JupyterLite playground
├── parachutist_problem.md   # Running example
├── datatypes.md             # Data types tutorial
├── variables.md             # Variables and operators
├── print.md                 # Print statements
├── comments.md              # Code comments
├── control_flow/            # If/else and loops
├── data_structures.md       # Lists, dicts, etc.
├── iterators.md             # Range, enumerate, zip
├── user_input.md            # Input from users
├── functions.md             # Defining functions
├── numpy_basics/            # NumPy introduction
├── errors.md                # Common Python errors
├── _static/
│   ├── mindmap.html         # Interactive mind map
│   └── parachutist_simulation.html  # Euler method simulation
├── notebooks/
│   └── playground.ipynb     # JupyterLite notebook
├── _config.yml              # Jupyter Book config
├── _toc.yml                 # Table of contents
└── .github/workflows/
    └── deploy.yml           # GitHub Actions deployment
```

---

## Deployment

The site automatically deploys to GitHub Pages on every push to `main` via GitHub Actions. The workflow:

1. Builds the Jupyter Book (classic v0.15.x)
2. Includes JupyterLite for in-browser Python
3. Deploys to GitHub Pages

---

## Contributing

Found a typo? Have a suggestion? Feel free to:
- Open an issue
- Submit a pull request
- Contact the course TA

---

## Author

**Krishna Patel**  
Teaching Assistant, CHL7002  
IIT Delhi

---

## License

This educational material is provided for CHL7002 students. Feel free to use it for learning purposes.
