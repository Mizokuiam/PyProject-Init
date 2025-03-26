# PyProject-Init

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python Versions](https://img.shields.io/badge/python-3.8%20%7C%203.9%20%7C%203.10%20%7C%203.11-blue)](https://www.python.org/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Checked with mypy](https://img.shields.io/badge/mypy-checked-blue)](http://mypy-lang.org/)
[![Linting: Ruff](https://img.shields.io/badge/linting-ruff-purple)](https://github.com/astral-sh/ruff)

> A powerful CLI tool to quickly generate standardized `pyproject.toml` files for Python projects with best-practice configurations.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Interactive Mode](#interactive-mode)
  - [Command Line Options](#command-line-options)
  - [Example Output](#example-output)
- [Default Configurations](#default-configurations)
- [Contributing](#contributing)
- [License](#license)

## Overview

Setting up a new Python project involves repetitive configuration tasks - creating a `pyproject.toml` file and configuring development tools like linters, formatters, testing frameworks, and type checkers. This process is time-consuming and error-prone.

**PyProject-Init** eliminates this friction by generating a complete, best-practice `pyproject.toml` configuration with a single command, allowing you to focus on writing code rather than project setup.

## Features

- **One-Command Setup**: Generate a complete `pyproject.toml` file with sensible defaults
- **Customizable**: Interactive prompts for project details and tool selection
- **Best Practices**: Pre-configured with industry-standard settings for:
  - **[Ruff](https://github.com/astral-sh/ruff)**: Fast Python linter and formatter
  - **[Black](https://github.com/psf/black)**: Uncompromising code formatter
  - **[Pytest](https://pytest.org/)**: Powerful testing framework with coverage reporting
  - **[Mypy](http://mypy-lang.org/)**: Static type checker
- **Consistent Structure**: Standardized project configuration across all your repositories
- **Time-Saving**: Eliminates manual configuration and reduces setup time from minutes to seconds

## Installation

### From Source (Current Method)

```bash
# Clone the repository
git clone https://github.com/Mizokuiam/PyProject-Init.git
cd PyProject-Init

# Create a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install in development mode (optional)
pip install -e .
```

### Via pip (Coming Soon)

```bash
pip install pyproject-init
```

## Usage

### Interactive Mode

Simply run the tool and follow the prompts:

```bash
# If installed with pip or in development mode
pyproject-init

# Or run directly
python pyproject_init.py
```

You'll be prompted for:

- **Project name**: The name of your Python package
- **Author name**: Your name or organization
- **Author email**: Contact email
- **Required Python version**: Minimum Python version (defaults to your current version)
- **Tool selection**: Choose which development tools to include

### Command Line Options

All options can be specified directly via command line arguments:

```bash
python pyproject_init.py --help
```

```
Usage: pyproject_init.py [OPTIONS]

  Generates a pyproject.toml file with selected development tools.

Options:
  --output-path PATH              Directory to save pyproject.toml in.
                                  [default: .]
  --project-name TEXT             Project name  [default: my-python-project]
  --author-name TEXT              Author name  [default: Your Name]
  --author-email TEXT             Author email  [default: your@email.com]
  --python-version TEXT           Required Python version (e.g., 3.10)
                                  [default: 3.10]
  --include-ruff / --no-include-ruff
                                  Include Ruff (linter/formatter)?  [default:
                                  include-ruff]
  --include-black / --no-include-black
                                  Include Black (formatter)?  [default:
                                  include-black]
  --include-pytest / --no-include-pytest
                                  Include Pytest (testing)?  [default:
                                  include-pytest]
  --include-mypy / --no-include-mypy
                                  Include Mypy (type checking)?  [default:
                                  include-mypy]
  --help                          Show this message and exit.
```

Example with direct options:

```bash
python pyproject_init.py --output-path ./my_project --project-name awesome-lib --author-name "Jane Doe" --no-include-black
```

### Example Output

After running the tool, you'll get a complete `pyproject.toml` file with your selected configurations:

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "my-python-project"
version = "0.1.0"
authors = [
    {name = "Your Name", email = "your@email.com"},
]
description = "A sample Python project"
readme = "README.md"
requires-python = ">=3.10"
classifiers = [
    "Programming Language :: Python :: 3.10",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]
dependencies = []

[project.optional-dependencies]
dev = [
    "ruff>=0.1.0,<1.0.0",
    "black>=23.0.0,<25.0.0",
    "pytest>=7.0.0,<9.0.0",
    "pytest-cov>=4.0.0,<6.0.0",
    "mypy>=1.0.0,<2.0.0",
]

# Tool configurations follow...
```

The tool also provides helpful output with example commands for using the configured tools.

## Default Configurations

PyProject-Init sets up sensible defaults for each tool:

### Ruff

```toml
[tool.ruff]
line-length = 88

[tool.ruff.lint]
select = ["E", "W", "F", "I", "UP", "C90", "B"]
ignore = []

[tool.ruff.format]
quote-style = "double"
```

### Black

```toml
[tool.black]
line-length = 88
target-version = ["py310"]
```

### Pytest

```toml
[tool.pytest.ini_options]
minversion = "7.0"
addopts = "-ra -q --cov=src --cov-report=term-missing"
testpaths = [
    "tests",
]
```

### Mypy

```toml
[tool.mypy]
python_version = "3.10"
warn_return_any = true
warn_unused_configs = true
ignore_missing_imports = true
exclude = ["build/", "dist/"]
```

## Contributing

Contributions are welcome! Here's how you can help:

1. **Report bugs or request features**: Open an issue describing what you'd like to see
2. **Submit improvements**: Fork the repository and create a pull request
3. **Enhance documentation**: Help improve the README or add more detailed guides
4. **Add new tool configurations**: Implement support for additional development tools

Potential areas for improvement:

- Support for additional tools (isort, bandit, etc.)
- More sophisticated configuration options
- Template generation for README, LICENSE, .gitignore files
- PyPI packaging
- Test suite for the generator itself

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/Mizokuiam">Mizokuiam</a>
</p>
