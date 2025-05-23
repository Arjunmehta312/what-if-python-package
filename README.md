# WhatIF Analyzer 🧪

A Python package for analyzing function behavior and edge cases through static analysis and automated testing.

## Features ✨

- Static analysis of function parameters and return types
- Automated edge case testing
- Detailed analysis reports
- Support for complex type hints
- Command-line interface
- Rich console output

## Requirements 📋

- Python 3.8 or higher
- Dependencies:
  - typing-extensions
  - inspect2
  - rich
  - click
  - pytest (for development)

## Installation 🚀

### From PyPI

```bash
pip install whatif-analyzer
```

### From Source

```bash
git clone https://github.com/Arjunmehta312/what-if-python-package.git
cd what-if-python-package
pip install -e .
```

For development installation with all dependencies:

```bash
pip install -e ".[dev]"
```

## Quick Start 🏃‍♂️

### Using the Decorator

```python
from whatif_analyzer import analyze

@analyze()
def calculate_discount(price: float, discount_percent: float) -> float:
    """Calculate the final price after applying a discount."""
    if discount_percent < 0 or discount_percent > 100:
        raise ValueError("Discount must be between 0 and 100")
    return price * (1 - discount_percent / 100)
```

### Using the CLI

```bash
whatif analyze path/to/your/module.py
```

### Using the API

```python
from whatif_analyzer import analyze_function

def my_function(x: int, y: float) -> str:
    return str(x + y)

report = analyze_function(my_function)
print(report)
```

## Example Report 📊

```
Function: calculate_discount
Parameters:
  - price: float
  - discount_percent: float
Return Type: float

Test Results:
✓ Test 1: price=0.0, discount_percent=0.0 → 0.0
✓ Test 2: price=100.0, discount_percent=50.0 → 50.0
✗ Test 3: price=-1.0, discount_percent=0.0 → ValueError
✓ Test 4: price=0.0, discount_percent=100.0 → 0.0
```

## Advanced Usage 🛠️

### Defining Custom Edge Cases

```python
from whatif_analyzer import analyze, EdgeCase

@analyze(edge_cases=[
    EdgeCase("price", [0, 100, 1000]),
    EdgeCase("discount_percent", [0, 50, 100])
])
def calculate_discount(price: float, discount_percent: float) -> float:
    return price * (1 - discount_percent / 100)
```

### Configuration Options

```python
@analyze(
    max_depth=3,
    include_none=True,
    timeout=5.0
)
def complex_function(x: int, y: float) -> str:
    # Your function here
    pass
```

## Testing 🧪

Run the test suite:

```bash
pytest
```

Run with coverage:

```bash
pytest --cov=whatif_analyzer
```

## Documentation 📚

For detailed documentation, visit our [documentation site](https://whatif-analyzer.readthedocs.io/).

## Contributing 🤝

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Run tests
5. Submit a pull request

## License 📄

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Citation 📝

If you use this package in your research, please cite:

```
@software{whatif_analyzer,
  author = {Arjun Mehta},
  title = {WhatIF Analyzer},
  year = {2024},
  url = {https://github.com/Arjunmehta312/what-if-python-package}
}
```

## Acknowledgments 🙏

- Thanks to all contributors
- Inspired by various testing and analysis tools

## Support 💬

- GitHub Issues: [Report bugs or request features](https://github.com/Arjunmehta312/what-if-python-package/issues)
- Documentation: [Read the docs](https://whatif-analyzer.readthedocs.io/)

## Changelog 📋

See [CHANGELOG.md](CHANGELOG.md) for a list of changes.

## Package Structure 📁

```
whatif-analyzer/
├── src/
│   └── whatif_analyzer/
│       ├── __init__.py
│       ├── analyzer.py
│       ├── cli.py
│       ├── edge_cases.py
│       ├── report.py
│       └── type_inference.py
├── tests/
│   ├── __init__.py
│   ├── test_analyzer.py
│   ├── test_cli.py
│   ├── test_edge_cases.py
│   ├── test_report.py
│   └── test_type_inference.py
├── pyproject.toml
├── setup.py
├── README.md
├── LICENSE
└── CHANGELOG.md
```

## PyPI Package 📦

This package is available on PyPI: [whatif-analyzer](https://pypi.org/project/whatif-analyzer/)